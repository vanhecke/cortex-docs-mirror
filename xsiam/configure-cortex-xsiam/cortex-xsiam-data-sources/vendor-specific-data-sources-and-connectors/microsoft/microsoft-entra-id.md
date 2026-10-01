---
description: Use Microsoft Entra ID data with Cortex XSIAM.
---

# Microsoft Entra ID

Monitor identity risks and secure identity configurations across your Microsoft Entra ID environment.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Identity Posture:** Maintain visibility and control over Microsoft Entra ID identities, including users, groups, roles, and granular permissions. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Security Posture:** Detect, monitor and alert on settings of your Microsoft Entra ID tenant. This capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your Microsoft Entra ID tenant. This sub-capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

### How to configure the Microsoft Entra ID data connector <a href="#how-to-configure-the-asana-connector" id="how-to-configure-the-asana-connector"></a>

Cortex XSIAM supports the following Microsoft Entra ID account plans:

* Microsoft Business Premium
* Microsoft Entra ID P1

To access Microsoft Entra ID, Cortex XSIAM requires the following information, which you will specify during the connection process:

* **Tenant ID**: A globally unique identifier (GUID) for your Microsoft Entra tenant.
* **Client ID**: Cortex XSIAM accesses the Microsoft Graph API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client ID to uniquely identify the application and its associated service principal.
* **Client Secret**: Cortex XSIAM accesses the Microsoft Graph API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client secret, which Cortex XSIAM uses to authenticate to the service principal.

Perform the following procedures in the order that they appear below.

#### **Task 1:** Create and register Your Microsoft Entra application

1. Open a web browser to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Log in to the administrator account.

Required Permissions: The administrator must be able to grant access to the API scopes required by SaaS Security.

3. From the left navigation pane in the Microsoft Entra admin center, select App registrations.
4. On the App registrations page, select **New application**.
5. On the Register an Application page, complete the following actions:
   1. Specify a name for the application.
   2. Select Accounts in this organizational directory only.
   3. Click **Register**. Microsoft Entra registers your application and displays the details page. Registering the application automatically creates its associated service principal.

#### Task 2: Copy the tenant details <a href="#step-3-copy-the-tenant-id-client-id-and-client-secret" id="step-3-copy-the-tenant-id-client-id-and-client-secret"></a>

1. Copy the tenant ID and client ID.
2. From the details page for your application, select **Overview**.
3. Copy the client ID from the Application (client) ID field and paste it into a text file.
4. Copy the tenant ID from the Directory (tenant) ID field and paste it into a text file. Do not continue to the next step unless you have copied the client ID and tenant ID. You will provide this information to Cortex XSIAM during the data connection process.
5. Create and copy the client secret.
6. From the details page for your application, select **Certificates & secrets > Client secrets**.
7. Select New client secret.
8. In the Add a client secret dialog, specify an expiration date for the client secret and click **Add**.
9. Copy the Value of the new client secret and paste it into a text file. Do not continue to the next step unless you have copied the client secret. You will need to provide this information to Cortex XSIAM during the data connection process.

#### Task 3: Configure API permissions  <a href="#step-4-configure-api-permissions-for-your-application" id="step-4-configure-api-permissions-for-your-application"></a>

Configure your application to enable access only to the Microsoft Graph API scopes that Cortex XSIAM requires.

1. From the details page for your application, select **API permissions**.
2. On the API permissions page, select **Add a permission**.
3. In the Request API permissions dialog, select the **Microsoft Graph API**.
4. Select Application permissions.
5. Select the following API scopes and click Add permissions:
   * AuthenticationContext.Read.All
   * IdentityProvider.Read.All
   * Policy.Read.All
   * RoleManagement.Read.Directory
6. On the API permissions page, verify that all the scopes were added as application permissions.
7. On the API permissions page, select **Grant admin consent** for your organization.

#### **Task 4:** Microsoft Entra ID **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Microsoft Entra ID.
4. Under **Recommended**, hover over the new Microsoft Entra ID integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, select the Service Principal option, then enter the Client ID, Client Secret, and Tenant ID.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Microsoft Entra ID is successfully connected. Confirm the Summary details and click **Save instance**.
