---
description: Use Intercom data with Cortex XSIAM.
---

# Intercom

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Intercom connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Intercom, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Access Token**: A unique, alphanumeric string that Intercom generates for an Intercom application that you create. The access token has the permissions that you specify in the Intercom application.
* **Region**: The region where Intercom is hosting your data.

#### **Task 1:** Generate and copy an access token <a href="#step-1-generate-and-copy-an-access-token" id="step-1-generate-and-copy-an-access-token"></a>

To generate the access token, you need to create an app in Intercom's Developer Hub.

1. Identify the Intercom account that you will use to create the Intercom app.

Required Permissions: To create the Intercom app, the account must be assigned to a role that has the Apps and Integrations Access permissions. This could be a custom Developer role or a role with greater permissions.

2. Open a web browser to the [Intercom login page](https://app.intercom.com/admins/sign_in) and log in to the account you identified.
3. Navigate to Intercom's Developer Hub:
   1. Click the settings icon (gear icon) in the lower-left corner of the window.
   2. From the Settings navigation pane, select **Integrations > Developer** Hub. The Your apps page lists any Intercom apps that you have created.
   3. On the Your apps page, click **New app**.
4. In the New app dialog, complete the following actions:
   1. Specify an **App Name**. Give it a meaningful name, such as Cortex XSIAM Integration Token.
   2. Select the **Workspace** where you want to add the app.
   3. Click **Create app**. Intercom displays a configuration page for the new app.
5. Edit your app to limit its permissions to the minimum that Cortex XSIAM requires. By default, your app has permission to all the data in your workspace.
   1. On the configuration page, make sure the Authentication tab is selected.
   2. On the Authentication page, click **Edit**.
   3. In the Workspace data area, deselect all the check boxes except for the Read admins check box.
6. Regenerate your access token. Intercom created an access token when you created your app, but that token was created before you modified the app's permissions. You must regenerate the token for the permission updates to take effect.
   1. In the left navigation pane, select **Test and publish > Your workspaces**.
   2. On the Your workspaces page, locate the access token and click **Regenerate token**.
   3. A confirmation dialog warns you that regenerating the token will delete the current token. Confirm that you want to Regenerate the token.
   4. On the Your workspaces page, copy the access token and paste it into a text file. Do not continue to the next step unless you have copied the access token. You must provide this token to Cortex XSIAM during the onboarding process.

#### Task 2: Identify your Intercom region <a href="#step-2-identify-your-intercom-region" id="step-2-identify-your-intercom-region"></a>

Use the following table to determine, based on your login URL, the region where Intercom is hosting your data.

| URL                                                         | Region              |
| ----------------------------------------------------------- | ------------------- |
| [https://app.intercom.com](https://app.intercom.com/)       | US (United States)  |
| [https://app.eu.intercom.com](https://app.eu.intercom.com/) | EU (European Union) |
| [https://app.au.intercom.com](https://app.au.intercom.com/) | AU (Australia)      |

#### Task 3: Connect Intercom to Cortex XSIAM

1. In Cortex XSIAM, navigate to **Settings → Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the Add Data Sources or Integrations page, search for Intercom.
4. Under **Recommended**, hover over the new Intercom integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter your access token and region.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Intercom is successfully connected. Confirm the **Summary details** and click **Save instance**.
