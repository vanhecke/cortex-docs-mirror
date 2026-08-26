---
description: >-
  Connect an Office 365 instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard Office 365

For SaaS Security to detect posture risks in your Office 365 instance, you must onboard your Office 365 instance to SaaS Security. Through the onboarding process, SaaS Security connects to a Microsoft API and, through the API, scans your Office 365 instance at regular intervals. You can onboard an Office 365 app by using OAuth 2.0 authorization or by using a Microsoft Entra (formerly Azure) service principal.

**Note**: Connecting to Office 365 enables SaaS Security to scan settings at a high level based on Microsoft's Secure Score. For greater visibility into a particular application in the Office 365 product family, onboard the individual product app. To scan more settings for Microsoft Word, Microsoft PowerPoint, and Microsoft Excel, onboard Office 365 - Productivity Apps. Other products in the Office 365 product family have their own tiles on the Applications page and can be onboarded separately.

Use the method that matches your environment:

* [Method 1: OAuth 2.0 Authorization](https://docs.google.com/document/d/1EIc1VvKe4SEe6D7jGSeIc_PI5JdhlR6qPPcPrU8Mj70/edit#method-1-oauth-20-authorization) — SaaS Security redirects you to log in to Office 365 and grant access
* [Method 2: Service Principal](https://docs.google.com/document/d/1EIc1VvKe4SEe6D7jGSeIc_PI5JdhlR6qPPcPrU8Mj70/edit#method-2-service-principal) — SaaS Security connects through a Microsoft Entra application you create

***

### Method 1: OAuth 2.0 Authorization

SaaS Security gets access to your Office 365 instance through OAuth 2.0 authorization. During the onboarding process, you are prompted to log in to Office 365 and to grant SaaS Security the access it requires.

You have the option to connect with read-only permissions or with read and write permissions:

* Read-only permissions enable SaaS Security to perform configuration scans, risky account scans, and third-party plugin scans.
* Read and write permissions enable additional features, including the ability to revoke a user's access to a third-party plugin, force a user out of their current SaaS application sessions from the Identity Security dashboard, and revoke a meeting bot's access to calendar applications from the Meetings dashboard.

Required Permissions: The account must be assigned to the Global Administrator role.

#### Step 1: Identify the Account for Granting SaaS Security Access

1. Identify the Office 365 account that you will use to log in to Office 365 during onboarding. SaaS Security uses this account to establish a connection to your Office 365 instance.
2. Log out of all Microsoft accounts. Logging out helps ensure that you log in under the correct account during the onboarding process. To prevent the browser from using saved credentials, you can open Cortex in an incognito window.

#### Step 2: Connect SaaS Security to Your Office 365 Instance (OAuth 2.0)

By adding an Office 365 app in Cortex, you enable SaaS Security to connect to your Office 365 instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Office 365 tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Specify whether you want SaaS Security to connect with Read Permissions only or with Read and Write permissions. The onboarding page lists the API scopes that SaaS Security will access.
7. Click Connect with Office 365. SaaS Security redirects you to the Office 365 login page.
8. Enter the credentials for the Microsoft account you identified and sign in to Office 365. Microsoft displays a consent form that details the access permissions that SaaS Security requires.
9. Review the consent form and allow the requested permissions. SaaS Security connects to your Office 365 instance and displays whether it was able to access the API scopes required for its scans and actions.

***

### Method 2: Service Principal

SaaS Security gets access to your Office 365 instance through a Microsoft Entra service principal, which represents a Microsoft Entra application that you create. You configure the application's permissions to give SaaS Security access to the API scopes it requires.

To onboard your Office 365 instance using a service principal, SaaS Security requires the following information.

| Item          | Description                                                                                                                                                                                                                                           |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tenant ID     | A globally unique identifier (GUID) for your Microsoft Entra tenant.                                                                                                                                                                                  |
| Client ID     | SaaS Security accesses a Microsoft API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client ID to uniquely identify the application and its associated service principal. |
| Client Secret | SaaS Security accesses a Microsoft API through a Microsoft Entra service principal that represents an application that you create. Microsoft Entra generates the client secret, which SaaS Security uses to authenticate to the service principal.    |

Required Permissions: The administrator must be able to grant access to the API scopes required by SaaS Security. These scopes differ depending on whether you want to grant read-only or read and write permissions.

**Note**: After SaaS Security connects to your Office 365 instance, it performs an initial scan and then runs scans at regular intervals. The service principal must remain available for scans to continue. If you delete the service principal, scans will fail and you will need to onboard Office 365 again.

#### Step 1: Log In to the Microsoft Entra Admin Center

1. Open a web browser to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Log in to the administrator account.

#### Step 2: Create and Register Your Microsoft Entra Application

1. From the left navigation pane, select Enterprise applications.
2. On the Enterprise applications page, select New application.
3. On the All applications page, select Create your own application.
4. On the Create your own application flyout dialog, complete the following actions:
5. Specify a name for the application.
6. Select Register an application to integrate with Microsoft Entra ID (App you're developing).
7. Click Create.
8. On the Register an application window:
9. For supported account types, select Accounts in this organizational directory only.
10. Click Register. Registering the application automatically creates its associated service principal.

#### Step 3: Identify the Required API Scopes from Cortex

To configure the correct API permissions, first retrieve the required scopes from the SaaS Security onboarding screen.

1. Log in to Cortex.
2. Select Settings > Data Sources and Integrations > Add New and click the Office 365 tile.
3. Under Capabilities, enter a name and select Security Posture, then click Next.
4. Select the option for Service Principal. The onboarding page lists the API scopes that SaaS Security requires for read access and for read and write access. Copy the API scopes that you want to allow. **Note**: Do not continue to the next step unless you have copied the permissions. You will add these permissions to your application.
5. Click Cancel Onboarding. You will complete the onboarding process after you finish configuring your application.

#### Step 4: Configure API Permissions for Your Application

1. From the left navigation pane in the Microsoft Entra admin center, select Enterprise applications.
2. From the list of applications on the All applications page, open your application.
3. From the details page for your application, select Permissions.
4. On the Permissions page, click the Application registration link to go to the API permissions page.
5. On the API permissions page, click Add a permission.
6. On the Request API permissions flyout dialog, select Microsoft Graph > Application Permissions.
7. Select each of the API scopes that you obtained from the Office 365 onboarding screen in Cortex and click Add permissions.
8. On the API permissions page, verify that all the scopes were added as application permissions. The scopes you added should all have a type of Application. Only the User.Read permission (added automatically by Microsoft Entra) will have a type of Delegated.
9. On the API permissions page, select Grant admin consent for your organization.

#### Step 5: Copy the Application Credentials and Tenant ID

1. Copy the client ID:
   1. From the details page for your application, select Overview.
   2. Copy the client ID from the Application (client) ID field and paste it into a text file.

Note: Do not continue to the next step unless you have copied the client ID. You will provide this information to SaaS Security during the onboarding process.

2. Create and copy the client secret:
   1. From the details page for your application, select Certificates & secrets > Client secrets.
   2. Create a New client secret.
   3. Copy the Value of the new client secret and paste it into a text file.

Note: Do not continue to the next step unless you have copied the client secret. You will provide this information to SaaS Security during the onboarding process.

3. Copy the tenant ID:
   1. From the left navigation pane in the Microsoft Entra admin center, select Home.
   2. Copy the tenant ID and paste it into a text file.

**Note**: Do not continue to the next step unless you have copied your tenant ID. You will provide this information to SaaS Security during the onboarding process.

#### Step 6: Connect SaaS Security to Your Office 365 Instance (Service Principal)

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Office 365 tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Select the option for Service Principal.
7. Under **Connections**, enter the Client ID, Client Secret, and Tenant ID.
8. Depending on the API permissions that you configured for your application, specify whether you want SaaS Security to connect with Read Permissions only or with Read and Write Permissions.
9. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. Click **Next** to complete the onboarding validation process.
