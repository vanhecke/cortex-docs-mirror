---
description: Use Aha! data with Cortex XSIAM.
---

# Aha!

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Aha! connector

Cortex XSIAM connects to your Aha! using Okta SSO or Microsoft Azure credentials. Your organization must have Okta or Microsoft Azure as an identity provider to proceed with the connection. The Okta or Microsoft Azure account must be configured for multi-factor authentication (MFA) using one-time passcodes.\
\
To access Aha!, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **User email**: The login email address of the account that Cortex XSIAM will use to access Aha!. **Required permissions:** The user account must be assigned to both the Account and Billing administrator roles in Aha!.
* **Password**: The password for the login account.
* **Instance Host**: The custom domain for accessing your organization's Aha! account. You specify this domain when you sign up for an Aha! account, and it is included as part of the URL that you use to access the account.

If you're logging in through Okta, you must provide Cortex XSIAM with the following additional information:

* **Okta subdomain**: The Okta subdomain for your organization. The subdomain was included in the login URL that Okta assigned to your organization.
* **Okta 2FA secret**: A key that is used to generate one-time passcodes for MFA.

If you're using Azure Active Directory (AD) as your identity provider, you must provide Cortex XSIAM with the following additional information:

* **Azure 2FA secret**: A key that is used to generate one-time passcodes for MFA.

Perform the following procedures in the order they appear below.

#### Task 1: Gather MFA credentials and host name

1. Identify the Okta user account that Cortex XSIAM will use to access your Aha! application. The user account must be assigned to both the Account and Billing administrator roles in Aha!.
2. Get a secret key for MFA. The steps you follow to get the MFA secret key differ depending on the identity provider you're using to access the account.
   1. To access the account through **Okta**:
      1. Identify your Okta subdomain.
      2. Generate and copy an MFA secret key.
   2. To access the account through **Microsoft Azure**:
      1. Enable third-party software OAuth tokens for the administrator account.
      2. Configure the account for MFA and copy the MFA secret key.
      3. Make note of your organization's Aha! instance host name.
3. Identify the instance host name. After you log in to Aha!, the instance host name is a unique subdomain included in the Aha! URL. The URL format is \<instance\_host>.aha.io.

#### Task 2: Connect Aha! to Cortex XSIAM

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Aha!.
4. Under **Recommended**, hover over the new Aha! integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, provide the Instance Host Name, Client ID, and Client Secret to authorize the connection.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Aha! is successfully connected. Confirm the Summary details and click **Save instance**.
