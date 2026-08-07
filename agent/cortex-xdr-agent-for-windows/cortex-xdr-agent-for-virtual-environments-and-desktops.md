---
description: >-
  Learn about the Cortex XDR agent virtual installation options and use the
  provided workflows to install the Cortex XDR agent on virtual Windows
  endpoints.
---

# Cortex XDR agent for virtual environments and desktops

### Cortex XDR agent virtual desktop infrastructure (VDI)

You can deploy Cortex XDR agents in virtual environments either as a standard installation, or as the following installations. Following the steps in the installation procedure is crucial for maintaining a fully functional and stable environment.

* **Non-persistent VDI installation**—Intended for non-persistent endpoints that replicate (also referred to as spawn) from a golden image that has the Cortex XDR agent installed. When a new VDI session starts and a connection to the internet is available, the endpoint uses the original golden image policy until the Cortex XDR agent retrieves the new policy from Cortex XDR and applies it after the first user logon. This may take up to 10 minutes. In addition, with VDI installation, the endpoint license returns to license pool either when the user logs off or ends the VDI session, or after a shorter timeout period than a standard Cortex XDR agent installation, thus ensuring that licenses are consumed only by active VDI. To install the Cortex XDR on non-persistent endpoints, follow the procedure to Configure the Cortex XDR Agent in a non-persistent VDI.
* **Persistent (Stateful) VDI installation**—For Cortex XDR agent installation on a Persistent VDI, follow the standard installation procedure for Windows endpoints.
* **Temporary session**—Intended for either physical or virtual endpoints (such as Microsoft Terminal Services) that repeatedly revert to a snapshot (or image) on which the Cortex XDR agent is not installed. After you install the Cortex XDR agent, Cortex XDR issues a license to the physical or virtual endpoint but will revoke the license after a short period of inactivity. When the machine reverts to the original state, and the Cortex XDR agent is reinstalled, the machine receives a license again. In a temporary session installation, the machine is protected by Cortex XDR from startup to shutdown, regardless of the time in which you logged on or off the machine. To install the Cortex XDR agent on a snapshot from which temporary sessions will spawn, configure the Cortex XDR agent for temporary sessions.

{% hint style="info" %}
### Note

VDI installation is intended for single-user scenarios, such as full desktop VDI. Temporary Session (TS) installation is best used for multi-user scenarios, such as terminal services.
{% endhint %}

<details>

<summary>How to configure the Cortex XDR agent in a non-persistent VDI</summary>

In non-persistent VDI mode, each session is temporary. When a user accesses a non-persistent virtual desktop and logs out, the virtual desktop is wiped clean and reverts back to the original pristine state of the golden image. The next time the user logs in, they receive a fresh image.

In non-persistent VDI mode, the machine exhibits the following behavior:

* **Licensing**—With non-persistent VDI endpoints, the Cortex XDR agent registers with Cortex XDR when the VDI instance boots. However the agent receives a license from the pool of available licenses and enforces endpoint protection only after the first user logon. To identify these endpoints for which protection is not yet available, Cortex XDR displays the status as **VDI Pending Log-on**. If the Cortex XDR agent does not perform a successful check-in within 1.5 hours since the user log-on, the agent reports back **Connection Lost** status. Cortex XDR automatically returns the license to the license pool when the user logs off, the agent is uninstalled, the session ends, or when the VDI is inactive. Revoking the license frees it up for use by another Cortex XDR agent.
* **Connectivity**—When the user logs on to the VDI machine, the Cortex XDR agent connects to Cortex XDR to receive the license and to obtain the relevant updates. The Cortex XDR agent continues to communicate with Cortex XDR throughout the life cycle of the VDI instance. The Cortex XDR agent only protects the machine when a user is logged in. When the user is logged out, the Cortex XDR agent disconnects from Cortex XDR. During this time, the Cortex XDR agent does not receive updated policies or verdicts and does not send heartbeat communications to Cortex XDR.
* **Storage**—In a non-persistent VDI, many VDI solutions allow you to choose either non-persistent or persistent storage. With non-persistent storage, the user settings and data are stored for the length of the session and are wiped clean when the session ends or a user logs out. With persistent storage, you can select folders or specific locations that persist after a session ends.

To ensure Cortex XDR correctly identifies and treats the agent as a VDI agent, perform the following workflow on the golden image:

1. Install any software that you plan to have on the VDI instances.
   1.  On the golden image, install the Cortext XDR agent for Windows and include the **`VDI_ENABLED=1`** VDI flag.

       For example:

       **`msiexec /i c:\install\cortexxdr.msi /l*v C:\temp\cortexxdrinstall.log /qn VDI_ENABLED=1`**
   2. Install additional required software.
2.  Scan your golden image for files and request verdicts.

    Use Cytool to scan your endpoint. We recommend this step to populate the golden image with verdicts for different file types. If you do not perform this step, the Cortex XDR agent has to evaluate each file when it attempts to run on an endpoint during each VDI session.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>As VDI machine scans are based on the golden image and additional files are examined upon execution, we recommend, for this case, that you disable scheduled scanning.</p></div>

    1. Open a command prompt as an administrator and navigate to `C:\Program Files\Palo Alto Networks\Traps`.
    2. If you plan to output the scanning report to the Cortex XDR folder, you must run the **`cytool protect disable`** command to disable Cortex XDR protection.
    3.  Run the **`cytool imageprep scan`** command, with any of the following optional parameters:

        * **` [timeout`` `` `**_**`<timeout in hours>`**_**`]`**—Number of hours you permit Cytool to run the scan (default is 4 hours).
        * **` [upload`` `` `**_**`<upload timeout in minutes>`**_**`]`**—Number of minutes that you permit Cytool to upload unknown files to assess the verdict (default is 95 minutes).
        * **` [path`` `` `**_**`<full path>`**_**`]`**—Path to the directory in which you want to output the scanning report.

        For example:

        **`cytool imageprep scan timeout 4 upload 60 path c:\report`**

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>If you need to install additional software after performing this step, you must re-scan the endpoint to allow the Cortex XDR agent to obtain verdicts for the new software.</p></div>
    4.  If you plan to use the Search and Destroy Malicious Files response action, you need to perform an additional scan to map all the files on the endpoint. Run the following commands and wait for them to complete:

        **`cytool file_system_scan start`**

        **`cytool file_system_scan query`**
    5. If you previously disabled service protection, enable it using the **`cytool protect enable`** command after the scan is complete.
    6. Review any portable executable (PE) files that WildFire^(®) determined to be malicious.
       1. Open the scan report in Microsoft Excel or an editor of your choice.
       2. Perform one of the following actions for each malicious PE file found:
          * Remove the malicious file from the golden image.
          * If you believe the WildFire verdict is incorrect, override the verdict for the PE file in Cortex XDR. Then perform a **Check In** from the Cortex XDR console on the golden image.
3. (Optional) If you later rename the golden image, you must run the **`cytool vdi update`** to update the golden image name and ID in the persistent database.
4. After the scripts execute, the machine will shut down, and the App Layering service will proceed to take the snapshot and complete the publishing process automatically.

</details>

<details>

<summary>How to configure the Cortex XDR agent for temporary sessions</summary>

To ensure Cortex XDR correctly identifies and manages the agent and associated licenses as a temporary session, perform the following to install the Cortex XDR agent on the snapshot:

*   Install the Cortex XDR agent for Windows and include the **`TS_ENABLED=1`** flag.

    For example:

    **`msiexec /i c:\install\cortexxdr.msi /l*v C:\temp\cortexxdrinstall.log /qn TS_ENABLED=1`**

</details>

### Cortex XDR agent compatibility with virtual applications

You can determine where to deploy the Cortex XDR agent using [Where can I install the Cortex XDR agent?](https://app.gitbook.com/s/fZ8QSMnkjnXpuOeuRcam/) in the Palo Alto Networks Compatibility Matrix. The following virtual applications require a unique installation workflow.

<details>

<summary>Citrix App layering</summary>

{% hint style="info" %}
### Note

Cortex XDR agent installations on the Application layer or User layer are not supported.
{% endhint %}

The Cortex XDR agent can be installed either on the Platform layer or on the OS layer. We recommend installation on the Platform layer. For best performance, all layers must be clean from any previous installations, use the Cortex XDR agent cleaner tool before proceeding.

{% hint style="warning" %}
### Prerequisites

Before installing Cortex XDR agent on the platform layer, ensure the following requirements are met:

* **App Layering Version:** The App Layering ELM version must be at least 2409.
{% endhint %}

To Install Cortex XDR agent follow these steps:

1. Install the Cortex XDR agent on the chosen layer (OS/Platform) during the preparation process of the App Layering image.
2.  Add the Cortex XDR agent to the Citrix App Layering exclusion list.

    Add the following entry to the Windows Registry: `HKLM\SYSTEM\CurrentControlSet\Services\Unirsd\ExcludeKey [REG_SZ] = "\Registry\Machine\System\Cyvera"`
3. Before finalizing the layer, run `cytool imageprep scan` [(see here for options)](#running-imageprep-for-citrix-non-persistent-vdis-that-utilize-citrix-app-layering) and then perform the extra steps as necessary for MCS or PVS provisioning shown below.

#### MCS provisioning (Cortex XDR agent on Platform Layer) - Admin controlled shutdown

On the Platform layer, create a specific text file to signal to Citrix to pause the shutdown process during image publishing.

`echo Cortex > C:\Windows\Setup\Scripts\kmsdir\Admin_Controlled_Shutdown.txt`

When Cortex XDR agent and all other platform layer requirements are installed, complete the setup by running the "Shutdown For Finalize" shortcut located on the desktop.

**During image publishing:**

1. Initiate the publishing process and watch the App Layering job details. Wait until the status reads, "Waiting for the virtual machine to be shutdown so a snapshot can be taken".
2. Connect to the running virtual machine.
3. Execute the following finalization commands in order:
   1. Update VDI: `cytool vdi update`.
   2. Run `cytool imageprep scan` [(see here for options)](#running-imageprep-for-citrix-non-persistent-vdis-that-utilize-citrix-app-layering)
   3.  Run the completion script as an administrator:

       `C:\Windows\setup\Scripts\kmsdir\CompleteDepoylment.cmd`.
4. When the scripts have finished running, the machine will shut down. The App Layering service will automatically capture the snapshot and finalize the publishing process.

{% hint style="info" %}
### Note

**Stalled UI Status:** If the `imageprep` scan takes more than six hours, the App Layering UI may show the status as **Stalled**. This is a known cosmetic issue and does not affect the successful publishing of the image.
{% endhint %}

#### **MCS Provisioning (Cortex XDR agent on OS layer)**

When the Cortex XDR agent is installed on the OS layer and you are using MCS for provisioning, the standard imageprep process cannot run automatically when the image is published. Instead, the only method to prepare the image is as follows:

1. Boot a machine using the newly created virtual disk (vDisk).
2. Manually run `cytool imageprep scan` [(see here for options)](#running-imageprep-for-citrix-non-persistent-vdis-that-utilize-citrix-app-layering)
3. Create a new vDisk from this now-prepared machine.

#### **PVS Provisioning (Cortex XDR agent on Platform layer and OS layer Installations)**

1. To successfully execute imageprep on a PVS vDisk, the vDisk must first be booted on a VDI instance with read/write access enabled.
2. Run `cytool imageprep scan` [(see here for options)](#running-imageprep-for-citrix-non-persistent-vdis-that-utilize-citrix-app-layering)
3. When the the imageprep process is completed, revert the vDisk to read-only mode for normal use.

#### Running imageprep for Citrix non-persistent VDI's that utilize Citrix App Layering

The imageprep process makes non-persistent VDIs run faster. It does this by scanning the entire disk and saving security information about system files. If you don't run this process, VDI performance may be affected.

To make sure imageprep works well, start the scan only when all layers are combined and can be accessed. How you start this process is different depending on whether you are using Machine Creation Services (MCS) or Provisioning Services (PVS).

1.  Run the **`cytool imageprep scan`** command, with any of the following optional parameters:

    * **` [timeout`` `` `**_**`<timeout in hours>`**_**`]`**—Number of hours you permit Cytool to run the scan (default is 4 hours).
    * **` [upload`` `` `**_**`<upload timeout in minutes>`**_**`]`**—Number of minutes that you permit Cytool to upload unknown files to assess the verdict (default is 95 minutes).
    * **` [path`` `` `**_**`<full path>`**_**`]`**—Path to the directory in which you want to output the scanning report.

    Example 1.

    **`cytool imageprep scan timeout 4 upload 60 path`` c:\report`**

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>If you need to install additional software after performing this step, you must re-scan the endpoint to allow the Cortex XDR agent to obtain verdicts for the new software.</p></div>
2.  Return to complete the instruction depending on which provisioning process you are using.

    [MCS provisioning (Cortex XDR agent on Platform Layer)](#mcs-provisioning-cortex-xdr-agent-on-platform-layer-admin-controlled-shutdown)

    [MCS provisioning (Cortex XDR agent on Platform Layer) - Admin controlled shutdown](#mcs-provisioning-cortex-xdr-agent-on-os-layer)

    [PVS Provisioning (Cortex XDR agent on Platform layer and OS layer Installations)](#pvs-provisioning-cortex-xdr-agent-on-platform-layer-and-os-layer-installations)

**Recommendations for non-persistent VDI image management**

For non-persistent VDI environments, after the vDisk is finalized, all automatic software updates (including operating system and user applications) should be disabled. If a software update is required, the image configuration procedure must be repeated, followed by rerunning the [imageprep](#running-imageprep-for-citrix-non-persistent-vdis-that-utilize-citrix-app-layering) procedure. Failure to follow this process may lead to performance degradation upon the initial launch of the updated application.

</details>

<details>

<summary>How to configure the Cortex XDR agent for VMWare app volumes</summary>

To deploy Cortex XDR agents with VMWare App Volumes, you must add Cortex XDR services to the App Volumes template exclusions list.

{% hint style="warning" %}
### Warning

Cortex XDR agent installations with VMWare App Volumes that are not performed according to this flow are not supported.
{% endhint %}

1.  Edit the **`Snapvol.cfg`** file.

    Follow the steps described in the [VMware Knowledge Base](https://kb.vmware.com/s/article/2149892) to locate, open, and edit the **`Snapvol.cfg`** file.
2.  Add Cortex XDR process exclusions to the App Volumes templates.

    Add the following Cortex XDR process exclusions to the App Volumes templates:

    ```screen
    ################################################################
    # Process exclusions
    ################################################################

    # Cortex Agent
    exclude_path=\Program Files\Palo Alto Networks\Traps

    exclude_path=\ProgramData\Cyvera
    ################################################################
    # 64-Bit OS exclusions
    ################################################################

    # Cortex Agent
    exclude_path=\Program Files (x86)\Palo Alto Networks\Traps

    ################################################################
    # Registry exclusions
    ################################################################

    #Cortex Agent
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\tlaservice
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\cyserver
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\cypatchdrv
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\cyveraservice
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\cyverak
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\cyvrfsfd
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\cyvrmtgn
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\telam
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\tedrdrv
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\tdevflt
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\twdservice
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\ControlSet001\services\tedrpers-*

    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\tlaservice
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\cyserver
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\cyveraservice
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\cyverak
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\cyvrfsfd
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\cyvrmtgn
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\telam
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\tedrdrv
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\tdevflt
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\twdservice
    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CurrentControlSet\services\tedrpers-*

    exclude_registry=\REGISTRY\MACHINE\SYSTEM\CYVERA
    exclude_registry=\REGISTRY\MACHINE\SOFTWARE\CYVERA
    exclude_registry=\REGISTRY\MACHINE\SOFTWARE\Palo Alto Networks\Traps
    ```
3. Create new AppStacks and Writable Volumes.
4.  Install the Cortex XDR agent on your virtual machines without any volumes attached.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Warning</h3><p>If you plan to mount any AppStacks and Writable Volumes that were made before the templates update to machines where the Cortex XDR agent is installed, you must update these volumes individually.</p></div>
5.  Verify the process.

    Check the new additions were added to the **`Snapvol.cfg`** file.

</details>
