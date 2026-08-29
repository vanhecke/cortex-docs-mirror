---
description: Use Aha! data with Cortex XSIAM.
---

# Aha!

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### Prerequisites

Complete the steps below on your Aha! instance to connect with Cortex.

Cortex connects to your Aha! instance using Okta SSO or Microsoft Azure credentials that you provide during the connection process. For this reason, your organization must be using Okta or Microsoft Azure as an identity provider. The Okta or Microsoft Azure account must be configured for multi-factor authentication (MFA) using one-time passcodes.\
\
Cortex logs in to Aha! instance using administrator account credentials. This account is used to scan your Aha! instance for misconfigured settings. If there are misconfigured settings, Cortex suggests a remediation action based on best practices.

To onboard your Aha! instance, complete the following actions:

1.  Collect information for accessing your Aha!  instance.

    To access your Aha!  instance, you will need the following information, which you will specify during the onboarding process:

    1. User email: The login email address of the account that SSPM will use to access your Aha!  instance. Required Permissions: The user account must be assigned to both the Account and Billing administrator roles in Aha!.
    2. Password: The password for the login account.
    3. Instance Host: The custom domain for accessing your organization's Aha!  account. You specify this domain when you sign up for an Aha!  account, and it is included as part of the URL that you use to access the account.

If you're logging in through Okta, you must provide SaaS Security with the following additional information:

* Okta subdomain: The Okta subdomain for your organization. The subdomain was included in the login URL that Okta assigned to your organization.
* Okta 2FA secret: A key that is used to generate one-time passcodes for MFA.

If you're using Azure Active Directory (AD) as your identity provider, you must provide Cortex with the following additional information:

* Azure 2FA secret: A key that is used to generate one-time passcodes for MFA.

As you complete the following steps, make note of the values of the items described in the preceding sections. You will need to enter these values during onboarding to access your Aha.io instance from SaaS Security.

1. Identify the Okta user account that SaaS Security will use to access your Aha! instance. The user account must be assigned to both the Account and Billing administrator roles in Aha.io.
2. Get a secret key for MFA. The steps you follow to get the MFA secret key differ depending on the identity provider you're using to access the account.
   1. To access the account through Okta:
      1. Identify your Okta subdomain.
      2. Generate and copy an MFA secret key.
   2. To access the account through Microsoft Azure:
      1. Enable third-party software OATH tokens for the administrator account.
      2. Configure the account for MFA and copy the MFA secret key.
      3. Make note of your organization's Aha.io instance host name.

After you log in to Aha!, the instance host name is a unique subdomain included in the Aha!  URL. The URL format is \<instance\_host>.aha.io.

### Configure Aha!&#x20;

Once you have setup your Aha! instance, follow the steps outlined in the Cortex Aha! data connector configuration wizard to complete the connection process. Provide the Tenant ID, Client ID, and Client Secret, of your Aha! instance, under the **Connections** step when prompted.
