---
description: >-
  Connect an Intercom instance to detect posture risks and compliance
  violations.
---

# Onboard Intercom

For SaaS Security to detect posture risks in your Intercom instance, you must onboard your Intercom instance to SaaS Security. Through the onboarding process, SaaS Security connects to an Intercom API by using an access token that you generate from the Intercom Developer Hub. After connecting to the Intercom API, SaaS Security scans your Intercom instance for misconfigured settings and account risks.

To access your Intercom instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item         | Description                                                                                                                                                                           |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Access Token | A unique, alphanumeric string that Intercom generates for an Intercom application that you create. The access token has the permissions that you specify in the Intercom application. |
| Region       | The region where Intercom is hosting your data.                                                                                                                                       |

To onboard your Intercom instance, complete the following actions.

***

### Step 1: Generate and Copy an Access Token

To generate the access token, you need to create an app in Intercom's Developer Hub.

1. Identify the Intercom account that you will use to create the Intercom app.

Required Permissions: To create the Intercom app, the account must be assigned to a role that has the Apps and Integrations Access permissions. This could be a custom Developer role or a role with greater permissions.

2. Open a web browser to the [Intercom login page](https://app.intercom.com/admins/sign_in) and log in to the account you identified.
3. Navigate to Intercom's Developer Hub:
   1. Click the settings icon (gear icon) in the lower-left corner of the window.
   2. From the Settings navigation pane, select Integrations > Developer Hub. The Your apps page lists any Intercom apps that you have created.
4. On the Your apps page, click New app.
5. In the New app dialog, complete the following actions:
   1. Specify an App Name. Give it a meaningful name, such as SaaS Security Integration Token.
   2. Select the Workspace where you want to add the app.
   3. Click Create app. Intercom displays a configuration page for the new app.
6. Edit your app to limit its permissions to the minimum that SaaS Security requires. By default, your app has permission to all the data in your workspace.
   1. On the configuration page, make sure the Authentication tab is selected.
   2. On the Authentication page, click Edit.
   3. In the Workspace data area, deselect all the check boxes except for the Read admins check box.
7.  Regenerate your access token. Intercom created an access token when you created your app, but that token was created before you modified the app's permissions. You must regenerate the token for the permission updates to take effect.

    1. In the left navigation pane, select Test and publish > Your workspaces.
    2. On the Your workspaces page, locate the access token and click Regenerate token.
    3. A confirmation dialog warns you that regenerating the token will delete the current token. Confirm that you want to Regenerate the token.
    4. On the Your workspaces page, copy the access token and paste it into a text file.

    **Note**: Do not continue to the next step unless you have copied the access token. You must provide this token to SaaS Security during the onboarding process.

***

### Step 2: Identify Your Intercom Region

Use the following table to determine, based on your login URL, the region where Intercom is hosting your data.

| URL                                                        | Region              |
| ---------------------------------------------------------- | ------------------- |
| [https://app.intercom.com](https://app.intercom.com)       | US (United States)  |
| [https://app.eu.intercom.com](https://app.eu.intercom.com) | EU (European Union) |
| [https://app.au.intercom.com](https://app.au.intercom.com) | AU (Australia)      |

***

### Step 3: Connect SaaS Security to Your Intercom Instance

By adding an Intercom app in Cortex, you enable SaaS Security to connect to your Intercom instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Intercom tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your access token and region.
7. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
