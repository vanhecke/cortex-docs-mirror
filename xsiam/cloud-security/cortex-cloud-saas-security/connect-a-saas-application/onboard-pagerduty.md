---
description: >-
  Connect a PagerDuty instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard PagerDuty

For SaaS Security to detect posture risks in your PagerDuty instance, you must onboard your PagerDuty instance to SaaS Security. Through the onboarding process, SaaS Security logs in to PagerDuty using administrator account credentials. SaaS Security uses this account to scan your PagerDuty instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

To onboard your PagerDuty instance, complete the following actions:

* Collect information for accessing your PagerDuty instance
* Connect SaaS Security to your PagerDuty instance

***

### Step 1: Collect Information for Accessing Your PagerDuty Instance

To access your PagerDuty instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item                | Description                                                                                                                     |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| User                | The username or email address of the administrator account. Required Permissions: The user must be the PagerDuty Account Owner. |
| Password            | The password for the administrator account.                                                                                     |
| PagerDuty Subdomain | If your account has a personalized PagerDuty subdomain, the name of the subdomain.                                              |
| Region              | PagerDuty manages data centers in different geographical regions. You must specify your service region.                         |

If you are using Okta as your identity provider, you must also provide:

| Item            | Description                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| Okta subdomain  | The Okta subdomain for your organization, included in the login URL that Okta assigned to your organization. |
| Okta 2FA secret | A key used to generate one-time passcodes for MFA.                                                           |

If you are using Azure Active Directory (AD) as your identity provider, you must also provide:

| Item             | Description                                        |
| ---------------- | -------------------------------------------------- |
| Azure 2FA secret | A key used to generate one-time passcodes for MFA. |

As you complete the following steps, make note of the values of the items described in the preceding tables. You will need to enter these values during onboarding to access your PagerDuty instance from SaaS Security.

1. Identify the administrator account that SaaS Security will use to access your PagerDuty instance. The administrator must be the PagerDuty Account Owner. SaaS Security needs Account Owner permissions to monitor your PagerDuty instance.
2. Determine whether you want SaaS Security to log in to the administrator account directly, or through an identity provider. Using an identity provider adds an extra layer of security by requiring MFA using one-time passcodes. You can use Okta or Microsoft Azure as the identity provider.

* (For Okta login): Identify your Okta subdomain, then generate and copy an MFA secret key.
* (For Microsoft Azure login): Enable third-party software OATH tokens for the administrator account, then configure the account for MFA and copy the MFA secret key.

3. Determine if your organization has a personalized PagerDuty subdomain. You can determine this from your PagerDuty URL. If you have a personalized subdomain, it is prepended to your PagerDuty URL (for example, \<subdomain>.pagerduty.com).

**Note**: If you have a personalized subdomain, make note of it before you continue to the next step. You must provide this information to SaaS Security during the onboarding process. If you do not have a personalized subdomain, leave the associated field blank during the onboarding process.

4. Make note of your PagerDuty service region, which you can determine from your PagerDuty URL after you log in to your account. If the URL contains the string eu, your region is the European Union (EU). If the URL does not contain a region code, your region is the United States (US).

***

### Step 2: Connect SaaS Security to Your PagerDuty Instance

By adding a PagerDuty app in Cortex, you enable SaaS Security to connect to your PagerDuty instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the PagerDuty tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, specify how you want SaaS Security to connect to your PagerDuty instance: Log in with Credentials, Log in with Okta, or Log in with Azure.
7. When prompted, provide SaaS Security with the administrator credentials, PagerDuty subdomain, and PagerDuty service region. If you do not have a personalized subdomain, leave the PagerDuty subdomain field blank. If SaaS Security is connecting through an identity provider, specify the information needed for MFA.
8. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
9. Click **Next** to complete the onboarding validation process.
