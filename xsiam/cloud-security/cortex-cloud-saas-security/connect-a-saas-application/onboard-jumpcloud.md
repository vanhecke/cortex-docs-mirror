---
description: >-
  Connect a JumpCloud instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard JumpCloud

For SaaS Security to detect posture risks in your JumpCloud instance, you must onboard your JumpCloud instance to SaaS Security. Through the onboarding process, SaaS Security connects to a JumpCloud API by using an API key that you generate from the JumpCloud Admin Portal. After connecting to the JumpCloud API, SaaS Security scans your JumpCloud instance for misconfigured settings and account risks.

To access your JumpCloud instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item            | Description                                                                                                                                                                                                                       |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Key         | A unique, alphanumeric string that JumpCloud generates for a JumpCloud administrator account. SaaS Security uses the key to authenticate to the JumpCloud API. The API key inherits the permissions of the administrator account. |
| Organization ID | A unique identifier for your organization within the JumpCloud platform.                                                                                                                                                          |

To onboard your JumpCloud instance, complete the following actions.

***

### Step 1: Generate and Copy an API Key for Your Organization

1. Identify the JumpCloud account that you will use to create the API key.

Required Permissions: To create the API key, you must use an account assigned to the Administrator role in JumpCloud. The account must have API access enabled. To enable API access for the Administrator account, contact an administrator assigned to the Administrator with Billing role. Only administrators assigned to the Administrator with Billing role can enable API access for an Administrator account. The API key inherits the permissions of the Administrator account.

2. Using the credentials of the Administrator account, log in to the [JumpCloud Admin Portal](https://console.jumpcloud.com/login/admin).
3. Locate your profile icon in the upper-right corner of the page and select \<profile-icon> > My API Key.
4. In the API Key dialog, specify a Custom expiration date of 365 days and click Generate New API Key. JumpCloud generates and displays a new API key.
5. Copy the API key and paste it into a text file.

Note: Do not continue to the next step unless you have copied the API key. You must provide this key to SaaS Security during the onboarding process.

***

### Step 2: Identify Your Organization ID

1. In the JumpCloud Admin Portal, navigate to your Settings page. In the lower-left corner of the Admin Portal, click Settings.
2. On the Settings page, navigate to the Organization Profile tab.
3. Copy your Organization ID and paste it into a text file.

Note: Do not continue to the next step unless you have copied the Organization ID. You must provide this information to SaaS Security during the onboarding process.

***

### Step 3: Connect SaaS Security to Your JumpCloud Instance

By adding a JumpCloud app in Cortex, you enable SaaS Security to connect to your JumpCloud instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the JumpCloud tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your API Key and Organization ID.
7. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
