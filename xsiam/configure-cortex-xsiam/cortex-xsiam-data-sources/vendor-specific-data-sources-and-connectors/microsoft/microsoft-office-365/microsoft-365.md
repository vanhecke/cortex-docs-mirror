---
description: Use Microsoft 365 (new) data with Cortex XSIAM.
---

# Microsoft 365 (new)

Secure sensitive data, monitor configurations, and track identity risks across your Microsoft 365 environment, including OneDrive, SharePoint, Teams, and Entra ID.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Automation and Remediation:** Run automated workflows and remediation actions across Microsoft 365 services using Microsoft Graph. This capability is available with any active Cortex AgentiX, Cortex Cloud Runtime Security, Cortex XSIAM, Cortex XDR, or Cortex Cloud license.
* **Data Security:** Scan and protect data across the selected services. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Identity Posture:** Maintain visibility and control over Microsoft Entra ID identities, including users, groups, roles, and granular permissions. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Security Posture:** Detect, monitor and alert on security settings across the selected services. This capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings across the selected services. This sub-capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

To configure this connector, follow these steps:

<details>

<summary><strong>Security Posture</strong></summary>

### How to configure the Microsoft Office 365 connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

{% hint style="info" %}
Connecting to Microsoft 365 enables Cortex XSIAM to scan settings at a high level based on Microsoft's Secure Score. For greater visibility into a particular application in the Microsoft 365 product family, onboard the individual product app. To scan more settings for Microsoft Word, Microsoft PowerPoint, and Microsoft Excel, onboard Office 365 - Productivity Apps. Other products in the Microsoft 365 product family have their own tiles on the Applications page and can be onboarded separately.
{% endhint %}

To onboard your Microsoft 365 instance using a service principal, Cortex XSIAM requires the following information.

* **Tenant ID:** A globally unique identifier (GUID) for your Microsoft Entra tenant.
* **Client ID**: Cortex XSIAM accesses a Microsoft API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client ID to uniquely identify the application and its associated service principal.
* **Client Secret**: Cortex XSIAM accesses a Microsoft API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client secret, which Cortex XSIAM uses to authenticate to the service principal.\
  Required Permissions: The administrator must be able to grant access to the API scopes required by Cortex XSIAM. These scopes differ depending on whether you want to grant read-only or read and write permissions.

{% hint style="info" %}
After Cortex XSIAM connects to your Microsoft 365 instance, it performs an initial scan and then runs scans at regular intervals. The service principal must remain available for scans to continue. If you delete the service principal, scans will fail and you will need to onboard Microsoft 365 again.
{% endhint %}

**Task 1: Create and Register Your Microsoft Entra Application**

1. Log in to the administrator account.
2. On the Enterprise applications page, select **New application**.
3. From the left navigation pane, select **Enterprise applications**.
4. Open a web browser to the [Microsoft Entra admin center](https://entra.microsoft.com/).
5. On the All applications page, select **Create your own application**.
6. On the Create your own application flyout dialog, complete the following actions:
7. Specify a name for the application.
8. Select Register an application to integrate with Microsoft Entra ID (App you're developing).
9. Click **Create**.
10. On the Register an application window, for supported account types, select Accounts in this organizational directory only.
11. Click Register. Registering the application automatically creates its associated service principal.

**Task 2:  Configure API Permissions for Your Application**

1. From the left navigation pane in the Microsoft Entra admin center, select Enterprise applications.
2. From the list of applications on the All applications page, open your application.
3. From the details page for your application, select Permissions.
4. On the Permissions page, click the Application registration link to go to the API permissions page.
5. On the API permissions page, click **Add a permission**.
6. On the Request API permissions flyout dialog, select **Microsoft Graph > Application Permissions**.
7. Select each of the API scopes that you obtained from the Office 365 onboarding screen in Cortex and click Add permissions.
8. On the API permissions page, verify that all the scopes were added as application permissions. The scopes you added should all have a type of Application. Only the _User.Read_ permission (added automatically by Microsoft Entra) will have a type of Delegated.
9.  On the API permissions page, select Grant admin consent for your organization.



**Task 3: Copy the Application Credentials and Tenant ID**

1. Copy the client ID:
   1. From the details page for your application, select Overview.
   2. Copy the client ID from the Application (client) ID field and paste it into a text file. Do not continue to the next step unless you have copied the client ID. You will provide this information to Cortex XSIAM during the connection process.
2. Create and copy the client secret:
   1. From the details page for your application, select **Certificates & secrets > Client secrets**.
   2. Create a New client secret.
   3. Copy the Value of the new client secret and paste it into a text file. Do not continue to the next step unless you have copied the client secret. You will provide this information to SaaS Security during the onboarding process.
3. Copy the tenant ID:
   1. From the left navigation pane in the Microsoft Entra admin center, select Home.
   2. Copy the tenant ID and paste it into a text file. Do not continue to the next step unless you have copied your tenant ID. You will provide this information to SaaS Security during the onboarding process.

**Task 4: Connect Microsoft 365 to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Microsoft 365.
4. Under **Recommended**, hover over the new Microsoft 365 integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the Tenant ID, Client ID, and Client Secret.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Microsoft 365 is successfully connected. Confirm the Summary details and click **Save instance**.

</details>

### Prerequisite

#### 1. Global Administrator access to the Azure portal

Sign in to the [Microsoft Azure portal](https://portal.azure.com/) as a Global Administrator. Use the [Create a Microsoft Entra ID](microsoft-365/create-a-microsoft-entra-id) page to obtain the following values:

* **Tenant ID:** Directory ID for your Microsoft 365 tenant.
* **Client ID:** Application ID generated during app registration.
* **Client Secret:** Client secret generated for the registered application.

#### 2. Configure the Microsoft 365

Before configuring Microsoft 365, configure the **Microsoft** **365** to collect the Microsoft 365 Management Activity logs required for SharePoint Online and OneDrive scanning.

For detailed configuration steps, see [Configure the Microsoft Office 365](ingest-logs-from-microsoft-office-365).

{% hint style="info" %}
**Note**

This prerequisite is not required when configuring Microsoft Teams.
{% endhint %}

### How to configure the **Microsoft 365** connector

#### Task 1. Select services

1. In Cortex Cloud, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. On the **Add Data Source** page, search for **Microsoft 365 (New)**, hover over it, The new Microsoft 365 connector has the description: Multi-service security integration for Microsoft 365 including OneDrive, SharePoint, Teams, and Entra ID. Click **Add**.
4. In the wizard, select the Microsoft 365 services that you want to configure, such as:
   * **OneDrive for Business**
   * **SharePoint Online**
   *   **Microsoft Teams.**

       For detailed configuration steps for Microsoft Teams connector, see [Microsoft Teams](../microsoft-teams).

{% hint style="info" %}
**Note**

Select one or more services based on your requirements. You can onboard all three services or select only the services you need.
{% endhint %}

5\. Click **Next**.

#### Capabilities tab

1. Enter a unique name for the new connector instance.
2. Review the available capabilities and select **Data Security** to enable scanning and inventory collection across the selected repositories.
3. (Optional) Enable **Automation and Remediation** if you plan to use automated labelling with Microsoft Purview Information Protection (MIP).

{% hint style="info" %}
**Note**

**Identity Posture** is automatically enabled when **Data Security** is selected and cannot be disabled during setup. Identity Posture is required for user and group validation and cross-tenant exposure analysis.
{% endhint %}

4. Click **Next**.

#### Connection tab

1. On the **Connection** page, enter the **Tenant ID** and click **Apply**.
2. After the Tenant ID is validated, enter the **Client ID** and **Client Secret** in their respective fields.
3. Click **Test** to validate the connection settings.
4. If the connection is successful, the wizard displays a green **Verified** status indicator.

{% hint style="info" %}
**Note**

If validation fails because of incorrect field values, close the wizard and restart the workflow. The current wizard session cannot be reused after a validation failure.
{% endhint %}

5\. Click **Next** to proceed.

#### Summary tab

1. On the **Summary** page, verify that each selected capability displays a **Connected** status.
2. If validation succeeds, the wizard displays a **Verification Success** message.
3. Click **Create Instance** to create the Microsoft 365 connector.

#### Task 2. (Optional) Post verification

After onboarding is complete, verify asset discovery and data security findings.

#### 1. Verify discovered assets

1. Go to **Inventory** > **All Assets**.
2. Filter the asset list by setting **Provider** to **Microsoft 365**.
3. Verify that Cortex discovers the following supported asset types:
   * **Microsoft OneDrive:** Individual user cloud storage environments provisioned within the Microsoft 365 organization.
   * **Microsoft Document Library:** Document containers, document sets, and file repositories hosted in OneDrive and SharePoint.
   * **Microsoft SharePoint Site:** Root and sub-level team sites, communication sites, and site collections that contain collaborative files and permissions.
   * **Microsoft Teams Workspace:** Mapped to Active Directory (AAD) Groups containing Public, Private, or Shared Channels.
   * **Microsoft Personal Workspace:** Captures 1-on-1 Direct Messages (DMs) and multi-user Group Chats.

#### 2. Verify policy findings

1. Select a OneDrive or other supported asset to open the details panel.
2. Review the **Overview** tab for asset health and other details.
3. Go to **Findings** to review detected security findings, including:
   * **Sensitive Content Detections:** Sensitive data matches, such as financial data, health records, credentials, API tokens, credit card numbers, and personally identifiable information (PII), detected in files stored in OneDrive and SharePoint or in Microsoft Teams chat messages and conversations.
   * **Insecure Sharing and External Exposure:** Files and folders exposed through anonymous access links, such as **Anyone with the link**, organization-wide shared links, or external guest user access in OneDrive and SharePoint. This also includes sensitive information shared in Microsoft Teams chats or conversations with external users or guest users.
   * **Misconfigured Permissions and Excessive Exposure:** Overly permissive access controls, broken permission inheritance, or unrestricted access to sensitive OneDrive folders, SharePoint sites, and document libraries.

{% hint style="info" %}
**Note**

* Any user addition to or removal from a Microsoft Teams group chat may take up to **6 hours** to be reflected.
* ACLs for messages sent before a user is added to or removed from a Microsoft Teams group chat are not updated to reflect the membership change.
* After onboarding a connector, Cortex Cloud may take **24 hours to 7 days** to fully process the data and generate findings. If you attempt to re-onboard the same connector using the same credentials during this transition period, previously generated findings and other data may temporarily reappear.
{% endhint %}

### Troubleshooting

1. **Connector Health Monitoring**

If the connector health status shows a _**Warning**_ or _**Error**_, follow the instructions displayed in the `Connector Health` dialog box in the console. If the issue persists, contact Support for further assistance.

2. **Forward Scan / Real-Time Events**
   1. Ensure that the `ActivityFeed.Read` permission is configured for the enterprise application and has been granted admin consent.
   2. Verify that all application permissions specified in the documentation are configured and have been granted admin consent.
   3. Confirm that the log collector was onboarded with the SharePoint Online option selected.
   4. Ensure that the Microsoft Entra application’s client secret or certificate has not expired and that the enterprise application remains authorized.

### Exposure Definitions

Microsoft content is classified into four exposure categories:\
• **Internal**: Documents that are not shared or are shared only with specific members of the organization.\
• **Organization-Wide**: Documents shared with all members of the organization, such as through a “People in your organization” link or tenant-wide permissions.\
• **External**: Documents shared with one or more users outside the organization.\
• **Public**: Documents with an anonymous sharing link enabled, allowing anyone with the link to access them.
