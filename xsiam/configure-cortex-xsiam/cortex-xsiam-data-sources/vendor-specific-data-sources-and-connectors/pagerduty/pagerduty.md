---
description: Use PagerDuty data in Cortex XSIAM.
---

# PagerDuty

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture**: Detect, monitor and alert on settings of your SaaS application.
  * `saas-posture-config-remediation`: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the PagerDuty connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access PagerDuty, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **User**: The username or email address of the administrator account. \
  Required Permissions: The user must be the PagerDuty Account Owner.
* **Password**: The password for the administrator account.
* **PagerDuty Subdomain**: If your account has a personalized PagerDuty subdomain, the name of the subdomain.
*   **Region**: PagerDuty manages data centers in different geographical regions. You must specify your service region.



If you are using Okta as your identity provider, you must also provide:

* **Okta subdomain**: The Okta subdomain for your organization, included in the login URL that Okta assigned to your organization.
* **Okta 2FA secret**: A key used to generate one-time passcodes for MFA.

If you are using Azure Active Directory (AD) as your identity provider, you must also provide:

* **Azure 2FA secret**: A key used to generate one-time passcodes for MFA.

As you complete the following steps, make note of the values of the items described in the preceding tables. You will need to enter these values during onboarding to access your PagerDuty instance from Cortex XSIAM.

#### **Task 1: Gather** PagerDuty account information

1. Identify the administrator account that Cortex XSIAM will use to access your PagerDuty instance. The administrator must be the PagerDuty Account Owner. Cortex XSIAM needs Account Owner permissions to monitor your PagerDuty instance.
2. Determine whether you want Cortex XSIAM to log in to the administrator account directly, or through an identity provider. Using an identity provider adds an extra layer of security by requiring MFA using one-time passcodes. You can use Okta or Microsoft Azure as the identity provider.
   * (For Okta login): Identify your Okta subdomain, then generate and copy an MFA secret key
   * (For Microsoft Azure login): Enable third-party software OATH tokens for the administrator account, then configure the account for MFA and copy the MFA secret key.
3. Determine if your organization has a personalized PagerDuty subdomain. You can determine this from your PagerDuty URL. If you have a personalized subdomain, it is prepended to your PagerDuty URL (for example, \<subdomain>.pagerduty.com). If you have a personalized subdomain, make note of it before you continue to the next step. You must provide this information to Cortex XSIAM during the onboarding process. If you do not have a personalized subdomain, leave the associated field blank during the data connection process.
4. Make note of your PagerDuty service region, which you can determine from your PagerDuty URL after you log in to your account. If the URL contains the string _eu_, your region is the European Union (EU). If the URL does not contain a region code, your region is the United States (US).

#### **Task 2: Connect** PagerDuty **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for PagerDuty.
4. Under **Recommended**, hover over the new PagerDuty integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the following administrator credentials:
   * Email
   * Password
   * MFA Secret Key
   * Okta Subdomain
   * PagerDuty Subdomain
   * Region
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that PagerDuty is successfully connected. Confirm the Summary details and click **Save instance**.

