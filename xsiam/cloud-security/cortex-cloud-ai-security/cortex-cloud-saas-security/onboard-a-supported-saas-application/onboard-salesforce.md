---
description: >-
  Onboard Salesforce to Cortex XSIAM for SaaS security posture monitoring and
  compliance visibility.
---

# Onboard Salesforce

For SaaS Security to detect posture risks in your Salesforce instance, you must onboard your Salesforce instance to SaaS Security. Through the onboarding process, SaaS Security connects to a Salesforce API and, through the API, scans your Salesforce instance for misconfigured settings and account risks.

You can onboard your Salesforce instance through an interactive OAuth 2.0 Authorization flow or through a Salesforce External Client App.

* OAuth 2.0 Authorization relies on a Salesforce user account to authorize access through a browser-based login. This approach can be faster to set up and leverages any SSO or MFA requirements already established by your organization.
* External Client App authenticates using application credentials (Client ID and Client Secret), creating a persistent, system-to-system link that does not rely on OAuth refresh tokens.

Use the method that matches your environment:

* [Method 1: OAuth 2.0 Authorization](https://docs.google.com/document/d/1EIc1VvKe4SEe6D7jGSeIc_PI5JdhlR6qPPcPrU8Mj70/edit#method-1-oauth-20-authorization)
* [Method 2: External Client App](https://docs.google.com/document/d/1EIc1VvKe4SEe6D7jGSeIc_PI5JdhlR6qPPcPrU8Mj70/edit#method-2-external-client-app)

***

### Method 1: OAuth 2.0 Authorization

SaaS Security gets access to your Salesforce instance through OAuth 2.0 authorization. During the onboarding process, you are prompted to log in to Salesforce and to grant SaaS Security the access it requires.

Required information:

| Item         | Description                                                                                               |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Instance URL | The unique web address for your Salesforce instance. Format: https://\<instance\_name>.my.salesforce.com. |

#### Step 1: Identify Your Salesforce Instance URL

Make note of your organization's Salesforce instance (domain) URL. Your instance URL has the format https://\<instance\_name>.my.salesforce.com. Include the https:// prefix when you provide this URL to SaaS Security.

If necessary, locate your instance URL from the My Domain Settings page:

1. Click the settings icon (gear icon) in the upper-right corner of the page and select Setup.
2. From the Setup page's left navigation pane, select Company Settings > My Domain.
3. The Current My Domain URL field contains your instance URL.

#### Step 2: Identify the Salesforce Account and Configure Permissions

Identify the Salesforce account that you will use to log in to Salesforce during onboarding. We recommend using a dedicated service account. If you delete the service account or change its password, scans will fail and you will need to onboard Salesforce again.

During onboarding, SaaS Security gives you an option to connect with read-only permissions or with read and write permissions.

Permissions for Read Access (configuration scans, identity scans, risky account scans):

| Scan Type      | Required Permission                                                                              |
| -------------- | ------------------------------------------------------------------------------------------------ |
| Configuration  | API Enabled, View Health Check                                                                   |
| Risky Accounts | API Enabled (plus disable login with Salesforce credentials on the Single Sign-on Settings page) |
| Identity       | API Enabled, View Event Log Files, View Setup and Configuration, View All Users                  |

Additional Permissions for Write Access (third-party plugin scans and automated remediation):

| Scan Type / Remediation   | Required Permission                                           |
| ------------------------- | ------------------------------------------------------------- |
| Configuration Remediation | API Enabled, View Health Check, Download AppExchange Packages |
| Third-Party Plugins       | API Enabled, Download AppExchange Packages                    |

To grant permissions to the user account, add the permissions to a permission set and assign the permission set to the Salesforce user account:

1. From the setup home page, select Users > Permission Sets.
2. Create a new permission set or edit an existing one.
3. On the setup page for the permission set, locate the System area and navigate to System Permissions.
4. Enable the required permissions and save.
5. Assign the permission set to the Salesforce user account.

#### Step 3: Install the SaaS Security OAuth App in Salesforce

Important: In September 2025, Salesforce updated its security policy for connected OAuth apps. To onboard or re-authenticate to Salesforce, you must install the SaaS Security OAuth app in Salesforce. You only need to complete this step once per Salesforce instance.

Salesforce now requires connected OAuth apps to be formally installed. Because the SaaS Security connector uses the OAuth 2.0 flow (which creates an uninstalled OAuth app), you must navigate to the Connected Apps OAuth Usage page in Salesforce, locate the SaaS Security uninstalled OAuth app, and install it.

If you have never onboarded Salesforce to SaaS Security, first complete the Connect step below to have Salesforce create the uninstalled connected app, then return to install it.

#### Step 4: Connect SaaS Security to Your Salesforce Instance (OAuth 2.0)

By adding a Salesforce app in Cortex, you enable SaaS Security to connect to your Salesforce instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Salesforce tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Select the option for OAuth 2.0.
7. Enter your Instance URL.
8. Specify whether you want SaaS Security to connect with Read Permissions only or with Read and Write Permissions. The onboarding page lists the API scopes that SaaS Security will access.
9. Click Connect with Salesforce. SaaS Security redirects you to the Salesforce login page.
10. Log in to the Salesforce account. Salesforce displays a consent form that details the access permissions that SaaS Security requires.
11. Review the consent form and allow the requested permissions. SaaS Security connects to your Salesforce instance and displays whether it was able to access the required API scopes.

***

### Method 2: External Client App

The External Client App approach authenticates using application credentials (Client ID and Client Secret). This method offers long-term stability by creating a persistent, system-to-system link that does not rely on OAuth refresh tokens.

Required information:

| Item          | Description                                                                                                                                                                                          |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Instance URL  | The unique web address for your Salesforce instance. Format: https://\<instance\_name>.my.salesforce.com.                                                                                            |
| Client ID     | SaaS Security accesses the Salesforce API through an External Client App that you create in Salesforce. Salesforce generates the Client ID to uniquely identify this app.                            |
| Client Secret | SaaS Security accesses the Salesforce API through an External Client App that you create in Salesforce. Salesforce generates the Client Secret, which SaaS Security uses to authenticate to the API. |

#### Connect SaaS Security to Your Salesforce Instance (External Client App)

By adding a Salesforce app in Cortex, you enable SaaS Security to connect to your Salesforce instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Salesforce tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Select the option for External Client App.
7. Enter your Instance URL and the application credentials (Client ID and Client Secret).
8. Specify whether you want SaaS Security to connect with Read Permissions only or with Read and Write Permissions. The onboarding page lists the API scopes that SaaS Security will access.
9. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
10. Click **Next** to complete the onboarding validation process.
