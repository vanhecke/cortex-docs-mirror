# Create a Microsoft Entra ID

To integrate Microsoft 365 services with Cortex Cloud for Data Security and Posture Management, you must create a **Microsoft Entra ID service principal** (formerly Azure AD). The service principal requires specific Microsoft Graph API permissions based on the capabilities you plan to enable.

### Prerequisites

* **Global Administrator** access to the Microsoft Entra admin center or Azure portal.
* Access to the Microsoft 365 tenant that you want to onboard.

#### Task 1. Create a Service Principal

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) or the [Azure portal](https://portal.azure.com/) as a **Global Administrator**.
2. Navigate to **App registrations** > **New registration**.
3. Enter a descriptive name for the application, such as `Cortex-Cloud-Integration`.
4. For **Supported account types** drop down, select **Single Tenant Only \[Your Organisation].**
5. Click **Register**.
6. On the **Overview** page, note the following values:
   * **Application (client) ID**
   * **Directory (tenant) ID**
7. Navigate to **Certificates & secrets** > **New client secret**.
8. Create a client secret.
9. Copy the **Secret Value** and store it.

#### Task 2. Configure API Permissions

Add the required **Microsoft Graph** application permissions based on the Cortex Cloud capabilities you plan to enable.

To add a permission:

1. In the application registration, go to **API permissions**.
2. Click **Add a permission**.
3. Select **Microsoft Graph**.
4. Select **Application permissions**.
5. Search for and select the required permissions listed in the following sections. Click on **Add permissions** once all the required permissions are added to the list.

#### Microsoft 365 Data Security

These permissions are required to scan files for sensitive content across SharePoint and OneDrive repositories.

| Permission                   |
| ---------------------------- |
| `SensitivityLabels.Read.All` |
| `Files.Read.All`             |
| `User.Read.All`              |
| `Sites.Read.All`             |

#### Microsoft 365 and Entra ID Identity Posture

These permissions are required for user and group validation and for computing cross-tenant exposure scopes.

| Permission                      |
| ------------------------------- |
| `User.Read.All`                 |
| `Group.Read.All`                |
| `Application.Read.All`          |
| `RoleManagement.Read.Directory` |
| `AuditLog.Read.All`             |

#### Microsoft 365 Automation and Remediation

These permissions are required for automated remediation actions.

| Permissions                            |
| -------------------------------------- |
| `Files.ReadWrite.All`                  |
| `Sites.ReadWrite.All`                  |
| `InformationProtectionPolicy.Read.All` |

#### Microsoft Teams Data Security Permissions

These permissions are required for scanning sensitive data in Microsoft Teams channels and messages.

| Permissions               |
| ------------------------- |
| `Chat.Read.All`           |
| `Chat.ReadWrite.All`      |
| `ChatMessage.Read.All`    |
| `Group.Read.All`          |
| `Team.ReadBasic.All`      |
| `TeamMember.Read.All`     |
| `User.Read.All`           |
| `Channel.ReadBasic.All`   |
| `ChannelMessage.Read.All` |
| `ChannelMember.Read.All`  |

### Task 3. Grant Admin Consent

After adding all required API permissions:

1. On the **API permissions** page, click **Grant admin consent for \[Your Organization]**.
2. Confirm the consent request.
3. Verify that the status of all required permissions changes to **Granted**.

After completing these steps, use the **Directory (tenant) ID**, **Application (client) ID**, and **Client Secret** when configuring the Microsoft 365 connector in Cortex Cloud.
