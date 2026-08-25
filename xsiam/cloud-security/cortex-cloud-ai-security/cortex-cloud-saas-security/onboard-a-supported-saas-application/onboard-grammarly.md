---
description: >-
  Onboard Grammarly to Cortex XSIAM for SaaS security posture monitoring and
  compliance visibility.
---

# Onboard Grammarly

For SaaS Security to detect posture risks in your Grammarly instance, you must onboard your Grammarly instance to SaaS Security. Through the onboarding process, SaaS Security logs in to Grammarly using administrator account credentials. SaaS Security uses this account to scan your Grammarly instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

SaaS Security gets access to your Grammarly instance by using Okta SSO credentials that you provide during the onboarding process. For this reason, your organization must be using Okta as an identity provider. The Okta account must be configured for multi-factor authentication (MFA) using one-time passcodes.

To onboard your Grammarly instance, complete the following actions:

* Collect information for accessing your Grammarly instance
* Connect SaaS Security to your Grammarly instance

***

### Step 1: Collect Information for Accessing Your Grammarly Instance

To access your Grammarly instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item           | Description                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| User email     | An email address of an Okta user account. Required Permissions: The user must be a Grammarly administrator.                    |
| User Password  | The password for the Okta user account.                                                                                        |
| Okta Subdomain | The Okta subdomain for your organization. The subdomain was included in the login URL that Okta assigned to your organization. |
| MFA Secret Key | A key that is used to generate one-time passcodes for multi-factor authentication.                                             |

As you complete the following steps, make note of the values of the items described in the preceding table. You will need to enter these values during onboarding to access your Grammarly instance from SaaS Security.

1. Identify the Okta user account that SaaS Security will use to access your Grammarly instance. The user account must have administrator privileges in Grammarly. SaaS Security needs this administrator access to monitor your Grammarly instance. **Note**: Remember which account you will use to access your Grammarly instance through Okta SSO authentication from SaaS Security. You will provide the login credentials to SaaS Security during the onboarding process.
2. To access the administrator account using Okta credentials:
   1. Identify your Okta subdomain.
   2. Generate and copy an MFA secret key.

***

### Step 2: Connect SaaS Security to Your Grammarly Instance

By adding a Grammarly app in Cortex, you enable SaaS Security to connect to your Grammarly instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Grammarly tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter the user credentials, Okta domain, and MFA secret key for accessing your Grammarly instance.
7. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
8. Click **Nex**t to complete the onboarding validation process.
