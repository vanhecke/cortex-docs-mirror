# Microsoft Teams

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Data Security:** Scan and protect Microsoft Teams data across channel messages, chats, and shared files. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Security Posture:** Detect, monitor and alert on settings of your Microsoft Teams application. This capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your Microsoft Teams application. This sub-capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

To configure this connector, follow these steps:

#### Prerequisite

#### Global Administrator access to the Azure portal

Sign in to the [Microsoft Azure portal](https://portal.azure.com/) as a Global Administrator. Use the [Create a Microsoft Entra ID ](microsoft-office-365/microsoft-365-new/create-a-microsoft-entra-id)page to obtain the following values:

* **Tenant ID:** Directory ID for your Microsoft Teams tenant.
* **Client ID:** Application ID generated during app registration.
* **Client Secret:** Client secret generated for the registered application.

#### **How to configure the Microsoft Teams connector**

#### Task 1. Select services

1. In Cortex Cloud, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. On the **Add Data Source** page, search for **Microsoft Teams**, hover over it, The new Microsoft Teams connector has the description: Microsoft Teams integration for data security across channel messages, chats, and shared files | Microsoft Teams integration for security posture management.&#x20;
4. Click **Add**.

#### Capabilities tab

1. Enter a unique name for the new connector instance.
2. **Data Security** will get auto select to scan and protect Microsoft Teams data across channel messages, chats and shared files.
3. Click **Next**.

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
3. Click **Create Instance** to create the Microsoft Teams connector.

#### Task 2. (Optional) Post verification

After onboarding is complete, verify asset discovery and data security findings.

#### 1. Verify discovered assets

1. Go to **Inventory** > **All Assets**.
2. Filter the asset list by setting **Provider** to **Microsoft Teams**.
3. Verify that Cortex discovers the following supported asset types:
   * **Microsoft Teams Workspace:** Mapped to Active Directory (AAD) Groups containing Public, Private, or Shared Channels.

#### 2. Verify policy findings

1. Select a OneDrive or other supported asset to open the details panel.
2. Review the **Overview** tab for asset health and other details.
3. Go to **Findings** to review detected security findings, including:
   * **Sensitive Content Detections:** Sensitive data matches, such as financial data, health records, credentials, API tokens, credit card numbers, and personally identifiable information (PII), detected in files stored in Microsoft Teams chat messages and conversations.
   * **Insecure Sharing and External Exposure:** includes sensitive information shared in Microsoft Teams chats or conversations with external users or guest users.

{% hint style="info" %}
**Note**

* Any user addition to or removal from a Microsoft Teams group chat may take up to **6 hours** to be reflected.
* ACLs for messages sent before a user is added to or removed from a Microsoft Teams group chat are not updated to reflect the membership change.
* After onboarding a connector, Cortex Cloud may take **24 hours to 7 days** to fully process the data and generate findings. If you attempt to re-onboard the same connector using the same credentials during this transition period, previously generated findings and other data may temporarily reappear.
{% endhint %}
