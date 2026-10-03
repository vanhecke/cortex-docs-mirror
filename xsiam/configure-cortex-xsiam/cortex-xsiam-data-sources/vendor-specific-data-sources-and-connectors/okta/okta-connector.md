---
description: Use Okta data in Cortex XSIAM.
---

# Okta connector

Secure identity configurations, monitor identity risks, and respond to threats across your Okta environment.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Identity Prevention: Trigger multi-factor authentication (MFA) challenges for users and anomalous access attempts identified by your Conditional Access Policy. This capability is available with any active Cortex Identity Threat license.
* Security Posture: Detect, monitor and alert on settings of your SaaS application. This capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application. This sub-capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

To configure this connector, follow the steps outlined in the configuration wizard.

<details>

<summary><strong>Security Posture</strong></summary>

### How to configure the Okta connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Okta, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **API Token**: A generated character string that identifies an Okta administrator to the Okta API. SaaS Security requires this API token to authenticate to the API. The token inherits the permissions of the administrator who creates it. Required permissions: For read and write access, the API token must be created by a Super Administrator. For read-only access, the API token can be created by a read-only administrator.
* **Admin Instance URL**: The URL for your administrator console.

#### **Task 1:** Create an Okta API Token

1. Identify the Okta administrator account that you will use to create your API token. The API token inherits the permissions of the administrator who creates it. For read and write access, create the token as a Super Administrator. For read-only access, create the token as a read-only administrator.
2. Using the administrator account that you identified, log in to your Okta administrator console.
3. Identify your administrator instance URL, which appears in the browser's address bar. Your administrator instance URL is your subdomain plus -admin.okta.com (format: https://\<subdomain>-admin.okta.com). Before you continue to the next step, make note of your administrator instance URL. You will provide this information to Cortex XSIAM during the onboarding process.
4. In the left navigation pane, select **Security > API**.
5. On the API page, select the Tokens tab.
6. Click **Create token**. A dialog opens prompting you to name your token.
7. Specify a name for your token and click **Create token**. Okta generates and displays your token.
8. Copy the generated token and paste it into a text file. Do not continue to the next step unless you have copied the API token. You will provide this token to Cortex XSIAM  during the onboarding process.

#### **Task 2:** Connect Okta to Cortex XSIAM

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Okta.
4. Under **Recommended**, hover over the new Okta integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the API key and personal access token details.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Okta is successfully connected. Confirm the Summary details and click **Save instance**.

</details>
