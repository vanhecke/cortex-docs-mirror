---
description: Connect a ClickUp instance to detect posture risks and compliance violations.
---

# Onboard ClickUp

For SaaS Security to detect posture risks in your ClickUp instance, you must onboard your ClickUp instance to SaaS Security. Through the onboarding process, SaaS Security logs in to ClickUp using administrator account credentials. SaaS Security uses this account to scan your ClickUp instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

To onboard your ClickUp instance, complete the following actions:

* Collect information for accessing your ClickUp instance
* Connect SaaS Security to your ClickUp instance

***

### Step 1: Collect Information for Accessing Your ClickUp Instance

To access your ClickUp instance, SaaS Security requires connection information. During the onboarding process, you specify the following required and optional information.

| User Email     | The login email address of a ClickUp administrator account. Required Permissions: The user must be assigned to the Admin role, or a role with greater permissions. |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Password       | The password for the ClickUp administrator account.                                                                                                                |
| MFA Secret Key | (Optional) A key that is used to generate one-time passcodes for multi-factor authentication.                                                                      |

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your ClickUp instance from SaaS Security.

1. Identify the ClickUp account that SaaS Security will use to access your ClickUp instance. Verify that the account is assigned to the Admin role, or a role with greater permissions.
2. (Optional) Generate and copy an MFA secret key.

MFA provides an extra layer of security when accessing the ClickUp administrator account. To enable this extra layer of security, the administrator account must be configured for MFA that uses time-based one-time passcodes. These one-time passcodes are generated from authenticator apps such as Google Authenticator by using an MFA secret key. Like an authenticator app, SaaS Security uses the MFA secret key for passcode generation.

1. Log in to your ClickUp administrator account.
2. Navigate to your My Settings page. Locate your account avatar in the lower-left corner of the page and select \<account-avatar> > My Settings.
3. On your My Settings page, locate the Two-factor authentication (2FA) section and turn on the toggle for Authenticator App (TOTP).
4. A pop-up is displayed, instructing you to install an authenticator app on your cellphone. Decide which authenticator app you will use and download it to your cellphone. After you install the authenticator, click Yes, ready to scan, but do not scan the QR code that is displayed.
5. A pop-up window displays your MFA key as a text string and also as a QR code. Copy and paste the MFA key text string into a text file so you can provide it to SaaS Security during onboarding. Then continue configuring your authenticator app by scanning the QR code or by manually entering the MFA key.

**Note**: MFA is optional. However, if you want SaaS Security to connect to the administrator account by using MFA, do not continue to the next step unless you have copied the MFA Secret Key. You will provide this key to SaaS Security during the onboarding process.

***

### Step 2: Connect SaaS Security to Your ClickUp Instance

By adding a ClickUp app in Cortex, you enable SaaS Security to connect to your ClickUp instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the ClickUp tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter the administrator login credentials and, optionally, the MFA secret key.
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.&#x20;
8. Click **Next** to complete the onboarding validation process.
