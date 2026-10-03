---
description: Use Sentry data in Cortex XSIAM.
---

# Sentry

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Security Posture**: Detect, monitor and alert on settings of your SAAS application.
  * **saas-posture-config-remediation**: Help remediate the misconfigured security settings of your SAAS application.

### How to configure the Sentry connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

Cortex XSIAM supports the Sentry _Business Plan_ account type.

To access Harness, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Personal Token**: A personal access token generated from a Sentry account. This unique alphanumeric string gives SaaS Security read-only access to organization and member data for a Sentry organization.

#### **Task 1: Generate a personal access token**

1. Identify the Sentry account you will use to generate the token.\
   Required permissions: No elevated permissions are required, but the account must be a member of the organization you want Cortex XSIAM to scan.
2. Open a browser to the [Sentry login page](https://sentry.io/auth/login/) and log in to the account you identified.
3. On the Sentry dashboard, open the account drop-down menu in the upper-left corner and select Personal Tokens.
4. On the Personal Tokens page, click **Create New Token**.
5. Select the following permission scopes for the token:
   * member:read
   * org:read
6. Enter a name for the token — for example, SaaS-Security-Integration-Token — then click **Create Token**.
7. Copy the personal access token and save it to a text file. Do not proceed to the next step until you have copied the personal token. You must provide this token during the onboarding process.

#### **Task 2: Connect** Sentry **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Sentry.
4. Under **Recommended**, hover over the new Sentry integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the API key and personal access token details.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Sentry is successfully connected. Confirm the Summary details and click **Save instance**.
