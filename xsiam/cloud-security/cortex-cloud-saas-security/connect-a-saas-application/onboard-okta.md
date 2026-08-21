---
description: Connect an Okta instance to detect posture risks and compliance violations.
---

# Onboard Okta

For SaaS Security to detect posture risks in your Okta instance, you must onboard your Okta instance to SaaS Security. Through the onboarding process, SaaS Security connects to an Okta API by using an API token that you generate from Okta's administrator console. After connecting to the Okta API, SaaS Security scans your Okta instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

During onboarding, SaaS Security gives you an option to connect with read-only permissions or with read and write permissions:

* Read-only permissions enable SaaS Security to perform read-only scans.
* Read and write permissions enable additional actions, such as automated remediation.

After SaaS Security establishes a connection to your Okta instance, it notifies you if it was unable to access certain API scopes. SaaS Security might not be able to access certain scopes if the user who created the API token lacked the required permissions.

To onboard your Okta instance, complete the following actions:

* Create an API token for connecting to your Okta instance
* Connect SaaS Security to your Okta instance

***

### Step 1: Create an API Token for Connecting to Your Okta Instance

To access your Okta instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item               | Description                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Token          | A generated character string that identifies an Okta administrator to the Okta API. SaaS Security requires this API token to authenticate to the API. The token inherits the permissions of the administrator who creates it. Required permissions: For read and write access, the API token must be created by a Super Administrator. For read-only access, the API token can be created by a read-only administrator. |
| Admin Instance URL | The URL for your administrator console.                                                                                                                                                                                                                                                                                                                                                                                 |

As you complete the following steps, make note of the values of the items described in the preceding table. You will enter these values during onboarding to enable SaaS Security to access your Okta instance.

1. Identify the Okta administrator account that you will use to create your API token. The API token inherits the permissions of the administrator who creates it. For read and write access, create the token as a Super Administrator. For read-only access, create the token as a read-only administrator.
2. Using the administrator account that you identified, log in to your Okta administrator console.
3. Identify your administrator instance URL, which appears in the browser's address bar. Your administrator instance URL is your subdomain plus -admin.okta.com (format: https://\<subdomain>-admin.okta.com).

**Note**: Before you continue to the next step, make note of your administrator instance URL. You will provide this information to SaaS Security during the onboarding process.

4. In the left navigation pane, select Security > API.
5. On the API page, select the Tokens tab.
6. Click Create token. A dialog opens prompting you to name your token.
7. Specify a name for your token and click Create token. Okta generates and displays your token.
8. Copy the generated token and paste it into a text file.

**Note**: Do not continue to the next step unless you have copied the API token. You will provide this token to SaaS Security during the onboarding process.

***

### Step 2: Connect SaaS Security to Your Okta Instance

By adding an Okta app in Cortex, you enable SaaS Security to connect to your Okta instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Okta tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your API token and your administrator instance URL.
7. Specify whether you want SaaS Security to connect with Read Permissions only or with Read and Write permissions. The onboarding page lists the API scopes that SaaS Security will access to complete its various scans and to perform remediation.
8. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
9. Click **Next** to complete the onboarding validation process.

