---
description: >-
  Learn about the Cortex XDR agent installation options and use the provided
  workflows to install the Cortex XDR agent on Windows endpoints.
---

# Install the Cortex XDR agent for Windows

Standard Cortex XDR agent installation is intended for standard physical endpoints or persistent virtual endpoints. Install Cortex XDR Agent using the MSI or from the command-line using Msiexec.

<details>

<summary>How to install Cortex XDR agent using the MSI</summary>

Use the following workflow to install the Cortex XDR agent using the MSI file.

1. Before installing the Cortex XDR agent on a Windows endpoint, verify that the system meets the requirements described in [the Cortex XDR Agent for Windows Requirements](cortex-xdr-agent-for-windows-requirements).
2. Download the Cortex XDR agent installer for Windows from Cortex XDR.
3.  Run the MSI file on the endpoint.

    The installer displays a welcome dialog.
4. Click **Next**.
5.  **Install** the agent.

    The installer displays a User Account Control dialog.
6. Click **Yes**.
7.  After you complete the installation, verify the Cortex XDR agent can establish a connection.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If the Cortex XDR agent does not connect to Cortex XDR, verify your internet connection and perform a check-in on the endpoint. If the agent still does not connect, verify that the installation package has not been removed from the Cortex XDR management console.</p></div>

</details>

<details>

<summary>How to install the Cortex XDR agent Using Msiexec</summary>

Msiexec provides full control over the installation process and allows you to install, modify, and perform operations on a Windows Installer from the command line interface (CLI). You can also use Msiexec to log any issues encountered during installation.

You can also use Msiexec in conjunction with a System Center Configuration Manager (SCCM), Altiris, Group Policy Object (GPO), or other MSI deployment software to install Cortex XDR on multiple endpoints for the first time.

When you install the Cortex XDR agent with Msiexec, you must install the Cortex XDR agent per-machine and not per-user.

Although Msiexec supports additional options, the Cortex XDR agent installers support only the options listed here. For example, with Msiexec, the option to install the software in a non-standard directory is not supported—you must use the default path.

{% hint style="info" %}
### Note

The following parameters apply to the initial installation on the Cortex XDR agent on the endpoint, except for the **`CLEAN_AGGRESIVLY=1`** parameter which should be used during agent upgrade.
{% endhint %}

* **`/i<installpath>\<installerfilename>.msi`**—Install a package. For example, **`msiexec /i c:\install\cortexxdr.msi`**.
* **`/qn`**—Displays no user interface (quiet installation).
* **`/L*v <logpath>\<logfilename>.txt`**—Log verbose output to a file. For example, **`/l*v c:\logs\install.txt`**.
* **`VDI_ENABLED=1`**—Use to install the Cortex XDR agent on the golden image for a non-persistent VDI. This option identifies the session as a VDI in Cortex XDR and applies license and endpoint management policy specific for non-persistent VDI. To set up the Cortex XDR agent on a golden image for non-persistent VDI, see [Cortex XDR agent for virtual environments and desktops](cortex-xdr-agent-for-virtual-environments-and-desktops).
* **`TS_ENABLED=1`**—Use to install the Cortex XDR agent on the golden image for a temporary session. This option identifies the session as a temporary session in Cortex XDR and to apply license and endpoint management policy specific for temporary sessions. To set up the Cortex XDR agent on a golden image for temporary sessions, see [Cortex XDR agent for virtual environments and desktops](cortex-xdr-agent-for-virtual-environments-and-desktops).
*   **`proxy_list`**—Use to install Cortex XDR agents that communicate with Cortex XDR through an application-specific proxy for Cortex XDR. This option is relevant in environments where Cortex XDR agents communicate with Cortex XDR through a proxy, enabling Cortex XDR admins to control and manage the agent proxy configuration settings without affecting the communication of other applications on the endpoint. To set up a Cortex XDR specific proxy, see _Configure Cortex XDR specific proxy_ section below. The Cortex XDR agent does not support proxy communication in environments where proxy authentication is required.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can also set up a system-wide proxy for all communication on the endpoint.</p></div>
*   **`RESTRICT_RESPONSE_ACTIONS=1`**—Use to permanently disable the option for Cortex XDR to perform all, or a combination, of the following actions on endpoints running a Cortex XDR agent: initiate a Live Terminal remote session on the endpoint, execute Python scripts on the endpoint, and retrieve files from the endpoint to Cortex XDR. Disabling any of these actions is an irreversible action, so if you later want to enable the action on the endpoint, you must uninstall the Cortex XDR agent and install a new package without this flag. To disable a specific action, use the corresponding flag:

    * **`RESTRICT_LIVE_TERMINAL=1`**—Use to disable Live Terminal.
    * **`RESTRICT_SCRIPT_EXECUTION=1`**—Use to disable script execution.
    * **`RESTRICT_FILE_RETRIEVAL=1`**—Use to disable files retrieval.

    To disable more than one option, use any combination of these flags.
* **`CLEAN_AGGRESIVLY=1`**—Use to clean the endpoint from a previous Cortex XDR agent installation that was performed in **`msi`** Advertise mode. For details, see [Cortex XDR Agents Deployed in Advertise Mode](troubleshooting-resources-for-windows/cortex-xdr-agents-deployed-in-advertise-mode).
* **`CONTENT={path}\content-XXX-XXXXX.zip`**—Use to install the Cortex XDR agent with the downloaded content file to ensure the agent can enforce policies and rules on the endpoint immediately after agent startup. For example, **`CONTENT=\\sccm\share\Traps\Version740\content-181-58641.zip`**. You can specify the content path either from the local volume or from a shared directory to which the current logged-in user has access. To understand the benefits, workflow, and requirements to support this type of deployment, refer to [Install the Cortex XDR Agent with Installer and Content Update Package](install-the-cortex-xdr-agent-with-installer-and-content-update-package).
* **`ENDPOINT_TAGS="Name1,Name2,Name3"`**—Use to add tags to the endpoint tags.

To install Cortex XDR using Msiexec:

1. Before installing the Cortex XDR agent on a Windows endpoint, verify that the system meets the requirements described in [Cortex XDR Agent for Windows Requirements](cortex-xdr-agent-for-windows-requirements).
2. Use one of the following methods to open a command prompt as an administrator.
   * Select Start → **All Programs** → **Accessories**. Right-click **Command prompt** and **Run as administrator**.
   * Select **Start**. In the **Start Search** box, type **cmd**. Then, to open the command prompt as an administrator, press **CTRL**+**SHIFT**+**ENTER**.
3.  Run the **`msiexec`** command followed by one or more supported options and properties.

    For example:

    **`msiexec /i c:\install\cortexxdr.msi /l*v C:\temp\cortexxdrinstall.log /qn`**

</details>

#### Configure Cortex XDR specific proxy

In environments where Cortex XDR agents communicate with Cortex XDR through a proxy, you can define a system-wide proxy that affects all communication on the endpoint, or a Cortex XDR specific proxy that you can set, manage, and disable in Cortex XDR. This topic describes how to install a Cortex XDR agent on the endpoint and assign it a Cortex XDR specific proxy.

{% hint style="info" %}
### Note

The Cortex XDR agent does not support proxy communication in environments where proxy authentication is required.
{% endhint %}

1.  Follow the procedure above to install the Cortex XDR agent using Msiexec and include the **`proxy_list`** argument.

    The argument format is **`proxy_list="<proxy>:<port>"`**

    1.  You can assign up to five different proxies per agent. For each proxy, enter the IP address and port number. You can also configure the proxy by entering the FQDN and port number. When you enter the FQDN, you can use both lowercase and uppercase letters. Avoid using special characters or spaces.

        For example:

        **`msiexec /i c:\install\cortexxdr.msi proxy_list="My.Network.Name:808,10.196.20.244:8080"`**
    2.  To install a Cortex XDR agent communicating through the Palo Alto Networks Broker Service you must enter the Broker VM IP address and a port number. You can use default port 8888 or set another port number.

        <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Warning</h3><p>You are not permitted to configure port numbers between 0-1024 and 63000-65000, or port numbers 4369, 5671, 5672, 5986, 6379, 8000, 9100, 15672, 25672. Additionally, you are not permitted to reuse port numbers you already assigned to the Syslog Collector applet.</p></div>
2. After the initial installation, you can change the proxy settings if necessary from the **Endpoints** page of Cortex XDR.
