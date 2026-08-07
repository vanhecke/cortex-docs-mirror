# Configure DLP end-to-end

This section describes how to get up and running with Cortex DLP, including how to define Endpoint DLP settings, add applications and application groups, and define data-in-motion rules.

### Onboarding checklist for DLP

We recommend following these steps to ensure all requirements for setting up DLP are met, protecting sensitive data, and maintaining compliance with your organization's standards.

{% stepper %}
{% step %}
### Step 1. Configure endpoint DLP settings

Configure endpoint DLP settings to define your organization's DLP setup.

See [Configure endpoint DLP settings](#configure-endpoint-dlp-settings).
{% endstep %}

{% step %}
### Step 2. Install the DLP browser extension

Install the DLP browser extension on your endpoint. This extension works with the DLP agent to monitor and enforce security policies on web-based activities.

See [Install DLP browser extension on your endpoint](#install-dlp-browser-extension-on-your-endpoint).
{% endstep %}

{% step %}
### Step 3. Check permissions for user roles

Verify that **Data Security Admin** can create, manage, and remove data-in-motion rules.

See [Check for permissions for user roles](../../onboard-cortex-xsiam/deployment-steps/set-up-users-and-roles/assign-user-roles-and-groups).
{% endstep %}

{% step %}
### Step 4. Add applications

Add local and web applications to the application group when selecting source and destination in the data-in-motion rule.

See [Create endpoint applications](#create-endpoint-applications).
{% endstep %}

{% step %}
### Step 5. Add application groups

Create application groups for the source and destination in the data-in-motion rule.

See [Create endpoint application groups](#create-endpoint-application-groups).
{% endstep %}

{% step %}
### Step 6. Define DLP rules

Rules control sensitive data transfers based on context. They can block, allow, or report transfers.

See [Create data-in-motion rules](#create-data-in-motion-rules).
{% endstep %}

{% step %}
### Step 7. DLP status in all endpoints

View the extension and DLP installation status on each endpoint.

See [DLP status in all endpoints](dlp-status-in-all-endpoints).
{% endstep %}

{% step %}
### Step 8. Review threats

Track and investigate issues triggered when a data-in-motion rule is violated.

See [Cortex DLP threat detection and issues](cortex-dlp-threat-detection-and-issues).
{% endstep %}
{% endstepper %}

### Configure endpoint DLP settings

Configure the endpoint DLP settings to manage your organization's DLP policies.

1. In **Default Actions & Thresholds**, there are two parts.
   1.  **Data-in-motion default action and threshold configurations**:

       Select the fallback policy for instances when the DLP process fails or times out:

       * **Allow file movement (fail-open)**: Allows the file transfer, preventing service interruption.
       *   **Block file movement (fail-close)**: Blocks the file transfer.

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When a fail-close action occurs, the system creates a <strong>Data movement blocked by Endpoint DLP fail-close action</strong> issue.</p></div>
   2.  **Auto disablement of rule threshold**

       This setting refers to rule suppression. When the number of hits exceeds the set number, the rule is disabled.

       Click **Reset** to revert to the default threshold as configured in the system.

       If a rule was suppressed, you can view details in **Settings** → **Management Audit Logs**.
2. For **Corporate Account Domain**, add the web application resources.
3. **Cortex Data Security Extension (Web DLP Channel)**: This option lets you manage browser extension installation and removal. Configure Chrome and Edge separately using one of the two modes. By default, MDM deploys the extension to selected endpoints. See the earlier instructions for installing the DLP browser extension.
   *   **MDM**: This default option distributes and installs the extension using a supported management tool, such as Microsoft Intune for Windows or JAMF for macOS.

       After installation, the agent communicates with the extension to activate endpoint DLP.
   *   **Forced activation (by XDR)**: This option installs a missing browser extension automatically. The endpoint must be associated with a domain.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>The agent does not force-install the extension if MDM already manages it on the endpoint.</li><li>The XDR agent force-installs the extension on managed and unmanaged browsers. If a browser later becomes organization-managed, redeploy the extension through the central management console.</li></ul></div>
   *   **Disable**: The extension is disabled.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>With MDM, the extension is user-managed. Cortex does not remove an installed MDM extension. It only disables communication with the DLP extension.</p></div>
4.  In the **End User Dialog** section, add the default pop-up message for these events:

    *   **Enable User Interaction**

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can specify the end-user message per rule.</p></div>
    * **Reporting Mismatch (FP)**
    * **Rule Override**

    For each option, enter the default text to display in the end-user dialog.

    * In the **Title**, enter the default dialog name.
    * In the **Body**, enter the dialog message. You can use the system default text. This also applies to **Reporting Mismatch** and **Rule Override**.
    * In the **Admin Email Link** field, enter the default admin email to include in the body.
    * In the **Dialog Main Button Label**, enter the text for the button that closes the window.

### Install DLP browser extension on your endpoint

To activate DLP, you must install the CDSx browser extension on your endpoint. This extension works with the DLP agent to monitor and enforce security policies on web-based activities.

{% hint style="info" %}
### Note

Extensions are not enabled in `Incognito` or `InPrivate` modes in Chrome and Edge. It is recommended to disable these modes in the organization.
{% endhint %}

#### Enabling the extension in Cortex

1. Navigate to **Modules** → **Data Security** → **Endpoint Data-in-Motion Rules** → **Endpoint DLP Settings**.
2. For **Cortex Data Security Extension (Web DLP Channel)**, select the browser extension activation mode. See [Configure endpoint DLP settings](#configure-endpoint-dlp-settings) for more information.

<details>

<summary>Windows</summary>

Use a managed deployment platform like UEM, MDM, or group policy to push the browser extension to the endpoints.

Refer to the steps below to download the registry file (reg file), install, and configure settings to activate the extension on the endpoints.

{% hint style="info" %}
### Important

Endpoints should be linked to the domain.
{% endhint %}

Select one of the following managed installation options:

**1. Managed installation from group policy**

Extension ID & URL:

`aalncdhjokfcbldaemnehledpfpibopi;file:///C:\ProgramData\Cyvera\Everyone\CDSX\extension.xml`

**2. Managed installation from Intune**

Extension ID & URL:

`aalncdhjokfcbldaemnehledpfpibopi;file:///C:\ProgramData\Cyvera\Everyone\CDSX\extension.xml`

**3. Managed installation on Edge**

You must first deploy the CDSx extension from the Microsoft Edge policy.

a. From the Microsoft 365 admin center, navigate to Settings+Microsoft Edge.

b. Select the **Configuration policies** tab, and select **+Create Policy**.

c. Enter a name (example: CDSx Extension Deployment), add an optional description, select the **Policy type**, and then click **Next**.

d. In **Settings**, select **+Add Setting**. Search and select the **ExtensionInstallForcelist** policy.

e. In **Control which extensions are installed silently**, paste `aalncdhjokfcbldaemnehledpfpibopi;file:///C:\ProgramData\Cyvera\Everyone\CDSX\extension.xml`, and then click **Next**.

f. In **Assignments**, select the target users or security groups, and then click **Next**.

g. Review the settings, and then click **Review and create**.

**4. Managed installation from the registry in Windows**

a. Install/uninstall the extension using the following files:

{% file src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FiRAULe8RTbfFeBb8uQ2g%2Fcdsx_install.reg.zip?alt=media&token=d58206a1-6350-4cb0-a604-74ba96162ae1" %}

{% file src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fd1W3MUusZjRGkUOrcyyt%2Fcdsx_uninstall.reg.zip?alt=media&token=21984018-74ec-4319-aa4c-582a1f0c309d" %}

b. Instead of step a, you can also add the following to the registry using `reg IMPORT <file.reg>`:

````
```programlisting
Windows Registry Editor Version 5.00

; ===== Start CDSX Policy
; Chrome
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\ExtensionSettings]

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\ExtensionSettings\aalncdhjokfcbldaemnehledpfpibopi]
"installation_mode"="force_installed"
"update_url"="file:///C:\\ProgramData\\Cyvera\\Everyone\\CDSX\\extension.xml"
"toolbar_pin"="force_pinned"

; Edge
[HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Edge\ExtensionSettings]

[HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Edge\ExtensionSettings\aalncdhjokfcbldaemnehledpfpibopi]
"installation_mode"="force_installed"
"update_url"="file:///C:\\ProgramData\\Cyvera\\Everyone\\CDSX\\extension.xml"
"toolbar_state"="force_shown"

; ===== End CDSX Policy
```
````

</details>

<details>

<summary>macOS</summary>

To enable the DLP browser extension on your endpoint, you must either create a configuration profile in JAMF or upload a predefined configuration profile in your MDM solution.

The predefined signed configuration profile includes settings that cannot be modified. An unsigned version is also available for self-signing.

{% hint style="info" %}
### Note

For a comprehensive overview, refer to the Cortex XDR Agent iOS Guide.
{% endhint %}

The following steps describe how to create a new configuration profile in JAMF to enable the DLP browser extension on your endpoint:

1. From **Configuration Profiles**, click **New**.
2. In the **General** page, enter a name and description.
3. From the left pane, under the **Options** tab, select **Application & Custom Settings** and then click **Upload**.
4. Add the following configuration details for each web browser:
   * **Chrome**:
     * **Preference Domain**: com.google.Chrome
     *   **Property List**:

         ```programlisting
         <?xml version="1.0" encoding="UTF-8"?>
         <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
         <plist version="1.0">
           <dict>
             <key>ExtensionSettings</key>
             <dict>
               <key>aalncdhjokfcbldaemnehledpfpibopi</key>
               <dict>
                 <key>installation_mode</key>
                 <string>force_installed</string>
                 <key>toolbar_pin</key>
                 <string>force_pinned</string>
                 <key>update_url</key>
                 <string>file:///Library/Application Support/PaloAltoNetworks/Traps/cdsx/extension.xml</string>
               </dict>
             </dict>
           </dict>
         </plist>
         ```
   * **Edge**:
     * **Preference Domain**: com.microsoft.Edge
     *   **Property List**:

         ```programlisting
         <?xml version="1.0" encoding="UTF-8"?>
         <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
         <plist version="1.0">
           <dict>
             <key>ExtensionSettings</key>
             <dict>
               <key>aalncdhjokfcbldaemnehledpfpibopi</key>
               <dict>
                 <key>installation_mode</key>
                 <string>force_installed</string>
                 <key>toolbar_state</key>
                 <string>force_shown</string>
                 <key>update_url</key>
                 <string>file:///Library/Application Support/PaloAltoNetworks/Traps/cdsx/extension.xml</string>
               </dict>
             </dict>
           </dict>
         </plist>
         ```
5. Click **Save**.

</details>

### Create endpoint applications

An effective data loss prevention (DLP) system allows an organization to define specific applications as sensitive. This enables the system to monitor and control the transmission of critical information, preventing its unauthorized release.

When creating a data-in-motion rule, you can specify the source of the sensitive data, but you must provide the intended destination. For the source and destination for the data-in-motion rule, you must select the relevant application groups ( custom local application group). The application groups comprise of predefined endpoint applications as defined by Palo Alto (local application).

Predefined applications are indicated by **Created by: Palo Alto Networks** in the **All Applications** table. For predefined applications, you do not see details such as **URLS/Domains**, **Process names**, **or signers**. You cannot edit or delete these applications.

The user can only create a Custom Web Application.

#### Endpoint application type:

After creating the application, you can select them from the application groups.

* **Predefined local applications**: The following apps and services are supported.
  * **FTP, SFTP and FTPS apps**:
    * FileZilla
    * OpenSSH
    * WinSCP
  * **SSH and RDP apps**:
    * PuTTY
* **Custom Web application**: In DLP, a web application refers to any software accessed via a web browser (e.g., cloud services, webmail, social media). Web DLP focuses on inspecting and controlling sensitive data as it travels over these internet-based channels, preventing unauthorized sharing or exfiltration. Palo Alto Networks has its own predefined list of applications. The Palo Alto predefined web applications cannot be edited or removed.

<details>

<summary>New custom web application</summary>

Add a custom web application that appears in the **Custom Web-Application Group** of the **Endpoint Application Groups**. You can select the source or destination when defining the data-in-motion rule.

1. Navigate to **Modules** → **Endpoint Data-in-Motion Rules** → **Endpoint Applications**.
2. Click **New Application** and select **Custom Web Application**.
3.  In **New Custom Web Application**, enter the application name, enter the URLs or domain of the web application, and then click ![dlp\_enter\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-da91c850f1cf117531fb89177763e316632430be%2Ff29c57040949b4776a932fa22d57630355271ebd69956315186b970629a493ec.png?alt=media).

    A web application is added to the list. You can add other custom web applications.
4.  After adding all the web applications, click **Add**.

    The web application is successfully added to the **All Applications** table as **Type: Web**.

Example:

* Web: custom URLs
* Local application: pre-defined applications
* Catalog: a special group that includes SAAS applications, categories
* Catalog web application groups: a special group that allows you to choose SAAS applications from the PANs catalog and to use the predefined catalog

</details>

### Create endpoint application groups

Data-in-motion rules require defining both a source and a destination, which can be specified using your predefined endpoint application groups.

Choose the relevant application group type.

*   **Catalog Web Application Group**: The catalog includes SAAS applications from PAN's predefined catalog and predefined web application categories.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The catalog lists all supported and tested applications. If an application you need is not on the list, contact support for assistance.</p></div>
*   **Custom Local Application Group**: Select the available options from the predefined local applications.

    For example: Unsanctioned chat apps.
*   **Custom Web Application Group**: Select the available options from the custom local applications. You can create a new web application.

    For example: AI chatbots.

### Create data-in-motion rules

You can create data-in-motion policies to identify, control, and protect sensitive information as it moves across networks, between systems, or to devices.

Each rule defines an action, **Allow**, **Block**, or **Report**, from a specified source to a web destination. Rule conditions must include the channel destination, [data profile](https://app.gitbook.com/s/HfNuZNmWlqy9Bl7fETmL/data-security/data-classification/how-to-disable-and-enable-data-profiles-in-cortex-data-classification), and type of data being accessed or moved. You can also configure responsive user dialogs for enforced events, which can be customized per rule.

To create a data-in-motion rule:

1. In **Modules** → **Data Security** → **Endpoint Data-in-Motion Rules** → **Data-in-Motion Rules,** click **Create New Rule**.
2. On the **General** page:
   1. Enter a unique name and description.
   2. Choose the **Action** to implement when the rule criteria are met, such as blocking the transfer or notifying relevant parties.
   3. Select the **Action for Partial Classification** to implement when partial classification occurs. Partial classification refers to a situation in which the classification process is incomplete, such as due to a timeout or a classification failure.
   4.  Select the **Severity** of the rule you are creating.

       The **Informational** action enables logging an activity without interfering with the user’s workflow.
   5. Enter a **Raised Issue Name** to use for the issue resulting from policy breaches.
   6. Select to **Disable/Enable Rule** as required.
3. On the **Context & Data** page:
   1.  For **Source**, select the Custom Web Application Groups.

       The source is the origin of the data, whether it resides on a local drive (such as a PDF on a laptop) or within a web application (such as a file in OneDrive).

       Without a defined source, this rule applies to every file by default. You can make the policy more targeted by selecting a specific source.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Third-party application behaviour:</p><ul><li>When a file upload is blocked, the local application may display its own generic error message in response to the DLP restriction. In similar cases, some third-party applications might still proceed by sending a dummy file or an error placeholder instead of the actual data.</li></ul></div>
   2.  For **Destination**, select the relevant Application Groups. See the earlier instructions for creating endpoint application groups.

       Selecting **Allow corporate accounts users to upload** lets corporate account users bypass the **Block** rule action and upload data from the web application.

       **USB Channel**: Select **File Write/Copy to USB** to enforce the rule on the USB device.
   3.  For **Data Scope**, select the relevant [Data Profile](https://app.gitbook.com/s/HfNuZNmWlqy9Bl7fETmL/data-security/data-classification/how-to-disable-and-enable-data-profiles-in-cortex-data-classification).

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>To maximize data security, if you use Microsoft Purview for extensive manual and automated file classification tagging and are looking to integrate those labels directly with the DLP policies to trigger protective actions based on a file's sensitivity, refer to <a href="https://app.gitbook.com/s/HfNuZNmWlqy9Bl7fETmL/data-security/data-classification/how-to-use-information-protection-labels-in-cortex-data-security">How to use information protection labels in Cortex Cloud Data Security</a>.</p></div>
4. On the **Target** page:
   *   For **Rule Target**, select the endpoints to which this rule will apply.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Distribution of the Endpoint DLP package is restricted to agents assigned to the data-in-motion policy. This ensures that only endpoints requiring DLP functionality are affected, rather than all eligible endpoints in the tenant.</p></div>
5. On the **User Interaction** page, you can add the default pop-up message for each of the following events.
   1. For **End User Dialog**, toggle **ON/OFF** to manage whether users see a message when the policy is violated.
   2. In the **Title**, enter the default name for the dialog.
   3.  In the **Body**, enter the message to display in the dialog. You can choose to use the system's default text. This is also relevant for **Reporting Mismatch** and **Rule Override**.

       If enabled, the **Rule Override** allows the user to override the block policy and temporarily retry the operation (to move the file again) to complete the action. The user's response is recorded as part of the **Issue**.
   4. In the **Admin Email Link**, enter the default admin email to be included in the body.
   5. In the **Dialog Main Button Label**, enter the text to use for the button to close the window.
6. Click **Next** to create the rule.
7. From the **Data-In-Motion Rules** table, click **Save** or move the rule down to change its priority, then click **Save**.

#### Rule priority

Cortex processes these rules sequentially from top to bottom. To ensure the correct outcome, place **Allow** rules above **Block** rules.

As soon as a first match is found for a data movement event, that rule's action is applied, and no other rules are evaluated for that specific event. Each matched event creates an **Issue**, and the total number of issues appears as **Hits** in the rules table.

Modify rule priority by dragging rules. If a conflict arises while setting a rule's priority, for example, if another user updates the policy simultaneously, Cortex saves the rule as a draft to prevent loss of your work.

#### Example: Creating a data-in-motion rule

An employee at Company X sends an attachment containing financial information to another employee's personal email address. This action violates the company’s data handling policy.

To help prevent this, you can create a data-in-motion rule with the following configuration:

| Field                        | Description                                                                                                                                                                                                                                                                                                                                     | Example user input                                  |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| **Rule Name**                | Provide a descriptive name for easy referencing.                                                                                                                                                                                                                                                                                                | Prevent Financial Data Transfer                     |
| **Action**                   | Specifies how data movement is controlled. Possible actions are: Block, Allow, or Report.                                                                                                                                                                                                                                                       | Block                                               |
| **Partial Classification**   | Select a fallback action if classification fails or exceeds a time threshold.                                                                                                                                                                                                                                                                   | Block                                               |
| **Severity**                 | Choose the severity level that the Issue will trigger. Possible options are: Critical, High, Medium, Low, Informational.                                                                                                                                                                                                                        | High                                                |
| **Raised Issue Name**        | The name appears on the Issues page when filtering for Endpoint DLP Issues.                                                                                                                                                                                                                                                                     | Blocked Financial File Transfer                     |
| **Source**                   | The web application group the data transfer originates from. You can create and manage these custom groups to suit your preferences.                                                                                                                                                                                                            | drive.google                                        |
| **Destination**              | Choose where the data is moving to. Possible options are: None, Any, Specific web application group.                                                                                                                                                                                                                                            | Web Application Group                               |
| **Local Application Groups** | Select apps through which users might transfer sensitive data.                                                                                                                                                                                                                                                                                  | Zoom, Slack, TeamViewer, and WhatsApp.              |
| **Data Profile**             | <p>Data Profiles are templates that define what kind of sensitive data to detect. Select the data profile to which the rule applies.</p><p>For more information, see <a href="../../cloud-security/cortex-cloud-data-classification/how-to-create-and-validate-a-custom-data-profile">How to create and validate a custom data profile.</a></p> | PHI, CCN (Credit Card Numbers), Financial, and PII. |
