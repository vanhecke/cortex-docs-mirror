---
description: >-
  Onboard Aha.io in Cortex XSIAM to track misconfigurations and application
  compliance.
---

# Onboard Aha.io

For SaaS Security to detect posture risks in your Aha.io instance, you must onboard your [Aha.io](http://aha.io) instance to SaaS Security. Through the onboarding process, SaaS Security logs in to Aha.io using administrator account credentials. This account is used to scan your Aha.io instance for misconfigured settings. If there are misconfigured settings, SaaS Security suggests a remediation action based on best practices.

SaaS Security gets access to your Aha.io instance by using Okta SSO or Microsoft Azure credentials that you provide during the onboarding process. For this reason, your organization must be using Okta or Microsoft Azure as an identity provider. The Okta or Microsoft Azure account must be configured for multi-factor authentication (MFA) using one-time passcodes.

\
To onboard your Aha.io instance, you must complete the following actions:

1. Collect information for accessing your Aha.io instance.

To access your Aha.io instance, you will need the following information, which you will specify during the onboarding process:

* User email: The login email address of the account that SSPM will use to access your Aha.io instance. Required Permissions: The user account must be assigned to both the Account and Billing administrator roles in Aha.io.
* Password: The password for the login account.
* Instance Host: The custom domain for accessing your organization's Aha.io account. You specify this domain when you sign up for an Aha.io account, and it is included as part of the URL that you use to access the account.

If you're logging in through Okta, you must provide SaaS Security with the following additional information:

* Okta subdomain: The Okta subdomain for your organization. The subdomain was included in the login URL that Okta assigned to your organization.
* Okta 2FA secret: A key that is used to generate one-time passcodes for MFA.

If you're using Azure Active Directory (AD) as your identity provider, you must provide SSPM with the following additional information:

* Azure 2FA secret: A key that is used to generate one-time passcodes for MFA.

As you complete the following steps, make note of the values of the items described in the preceding tables. You will need to enter these values during onboarding to access your Aha.io instance from SaaS Security.

2. Identify the Okta user account that SaaS Security will use to access your Aha.io instance. The user account must be assigned to both the Account and Billing administrator roles in Aha.io.
3. Get a secret key for MFA. The steps you follow to get the MFA secret key differ depending on the identity provider you're using to access the account.
4. (For Okta log in) To access the account through Okta:
   1. Identify your Okta subdomain.
   2. Generate and copy an MFA secret key.
5. (For Microsoft Azure log in) To access the account through Microsoft Azure:
   1. Enable third-party software OATH tokens for the administrator account.
   2. Configure the account for MFA and copy the MFA secret key.
   3. Make note of your organization's Aha.io instance host name.

After you log in to Aha.io, the instance host name is a unique subdomain included in the Aha.io URL. The URL format is \<instance\_host>.aha.io.

4. Connect SaaS Security to your Aha.io instance.
   1. Log in to Cortex.
   2. Select **Modules > SaaS Security > Add Data Source**. You can use the Search bar to find the app you wish to connect to.
   3. Click the Aha.io tile.
   4. Under **Capabilities**, Enter a Name for your application.
   5. Select Security Posture under Default Capabilities and click Next.
   6. Under **Connections**, provide the Tenant ID, Client ID, and Client Secret.
   7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
   8. Click **Next** to complete the onboarding validation process.
