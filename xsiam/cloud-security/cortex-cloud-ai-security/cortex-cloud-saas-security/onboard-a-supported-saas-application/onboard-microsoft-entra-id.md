---
description: >-
  Onboard Microsoft Entra ID to Cortex XSIAM for SaaS security posture
  monitoring and compliance visibility.
---

# Onboard Microsoft Entra ID

For SaaS Security to detect posture risks in your Microsoft Entra ID instance, you must onboard your Microsoft Entra ID instance to SaaS Security. Through the onboarding process, SaaS Security connects to the Microsoft Graph API and, through the API, scans your Microsoft Entra ID instance at regular intervals.

SaaS Security gets access to your Microsoft Entra ID instance through a service principal, which represents a Microsoft Entra application that you create. You configure this application's permissions to enable SaaS Security to access only the API scopes it requires to complete its scans. When you register this application, Microsoft Entra creates the associated service principal that SaaS Security uses to connect to the API.

The supported Microsoft account plans for SaaS Security scans are:

* Microsoft Business Premium
* Microsoft Entra ID P1

To access your Microsoft Entra ID instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item          | Description                                                                                                                                                                                                                                                   |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tenant ID     | A globally unique identifier (GUID) for your Microsoft Entra tenant.                                                                                                                                                                                          |
| Client ID     | SaaS Security accesses the Microsoft Graph API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client ID to uniquely identify the application and its associated service principal. |
| Client Secret | SaaS Security accesses the Microsoft Graph API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client secret, which SaaS Security uses to authenticate to the service principal.    |

To onboard your Microsoft Entra ID instance, complete the following actions.

***

### Step 1: Log In to the Microsoft Entra Admin Center

1. Open a web browser to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Log in to the administrator account.

Required Permissions: The administrator must be able to grant access to the API scopes required by SaaS Security.

***

### Step 2: Create and Register Your Microsoft Entra Application

1. From the left navigation pane in the Microsoft Entra admin center, select App registrations.
2. On the App registrations page, select New application.
3. On the Register an Application page, complete the following actions:
4. Specify a name for the application.
5. Select Accounts in this organizational directory only.
6. Click Register. Microsoft Entra registers your application and displays the details page. Registering the application automatically creates its associated service principal.

***

### Step 3: Copy the Tenant ID, Client ID, and Client Secret

1. Copy the tenant ID and client ID.
2. From the details page for your application, select Overview.
3. Copy the client ID from the Application (client) ID field and paste it into a text file.
4. Copy the tenant ID from the Directory (tenant) ID field and paste it into a text file. **Note**: Do not continue to the next step unless you have copied the client ID and tenant ID. You will provide this information to SaaS Security during the onboarding process.
5. Create and copy the client secret.
6. From the details page for your application, select Certificates & secrets > Client secrets.
7. Select New client secret.
8. In the Add a client secret flyout dialog, specify an expiration date for the client secret and click Add.
9. Copy the Value of the new client secret and paste it into a text file.

**Note**: Do not continue to the next step unless you have copied the client secret. You will need to provide this information to SaaS Security during the onboarding process.

***

### Step 4: Configure API Permissions for Your Application

Configure your application to enable access only to the Microsoft Graph API scopes that SaaS Security requires.

1. From the details page for your application, select API permissions.
2. On the API permissions page, select Add a permission.
3. In the Request API permissions flyout dialog, select the Microsoft Graph API.
4. Select Application permissions.
5. Select the following API scopes and click Add permissions:
   1. AuthenticationContext.Read.All
   2. IdentityProvider.Read.All
   3. Policy.Read.All
   4. RoleManagement.Read.Directory
6. On the API permissions page, verify that all the scopes were added as application permissions.
7. On the API permissions page, select Grant admin consent for your organization.

***

### Step 5: Connect SaaS Security to Your Microsoft Entra ID Instance

By adding a Microsoft Entra ID app in Cortex, you enable SaaS Security to connect to your Microsoft Entra ID instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Microsoft Entra ID tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, select the Service Principal option, then enter the Client ID, Client Secret, and Tenant ID.
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
