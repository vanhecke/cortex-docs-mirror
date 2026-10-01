---
description: Use Harness data with Cortex XSIAM.
---

# Harness

The capabilities and sub-capabilities listed for this connector are available with any active Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Harness connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Harness, Cortex XSIAM requires the following information, which you will specify during the connection process.

* API access key and personal access token

#### **Task 1: Gather** Harness access information

To access a Harness API, SaaS Security requires an API key that contains a personal access token of an administrator assigned to the Account Admin role. The API key inherits the permissions of the administrator who generates the key and token.

1. Open a web browser to the Harness site at [www.harness.io](https://www.harness.io/) and log in as an administrator assigned to the Account Admin role. Required Permissions: You must log in as an administrator assigned to the Account Admin role. The account must also have permission to View and to Create/Edit authentication settings.
2. To open your profile, click the profile icon in the lower-left corner of the window.
3. On your profile, click **+ API Key**. The New API Key dialog is displayed.
4. Enter a name for your key and click **Save**. The key appears in the My API Keys area.
5. For the new API key, click **+ Token**. The New Token dialog is displayed.
6. Enter a name and expiration date for the token and click **Generate Token**.
7. Harness generates and displays the personal access token. Copy and paste the token into a text file. Do not continue to the next step unless you have copied the token. When SaaS Security prompts you for an API key during the onboarding process, enter this personal access token.

#### **Task 2: Connect** Harness **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Harness.
4. Under **Recommended**, hover over the new Harness integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the API key and personal access token details.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Harness is successfully connected. Confirm the Summary details and click **Save instance**.
