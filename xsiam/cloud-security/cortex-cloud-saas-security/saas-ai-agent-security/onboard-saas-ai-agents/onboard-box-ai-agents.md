---
description: >-
  Connect Box AI Agents in Cortex XSIAM SaaS Agent Security for visibility and
  control across your AI ecosystem.
---

# Onboard Box AI Agents

**Prerequisites**

* Ensure you have the necessary administrative privileges in your Box instance, including the ability to access the Admin and Dev console.
* To access Box AI Studio and start building custom agents, your organization must have a Box - Enterprise Advanced license. If you would like to explore these capabilities, coordinate with your IT Administrator or Box Sales representative to ensure the proper licensing is in place.

**Note**: Box AI Studio is a Microsoft-native product, not a feature developed or managed by Palo Alto Networks.

* Ensure you have enabled Box AI. To do this, go to your **Box instance > Box AI > Settings** and click **Enable Box AI**.

1. Create and Configure a Custom Box App
   1. Sign in to your Box instance.
   2. From the left navigation pane, select Dev Console > Create Platform App > Custom App.
   3. On the Custom App page, enter the following information:
      1. Give a suitable App Name.
      2. Give a suitable Description (optional).
      3. For Purpose, choose Automation from the drop-down and click Next.
   4. Select Server Authentication (Client Credentials Grant) for the authentication method and click Create App.
   5. On the newly created app page, select the Configuration tab.
   6. In the OAuth 2.0 Credentials section, copy the Client ID and the Client Secret (Fetch Client Secret) and keep it handy for use during onboarding.
   7. In the App Access Level section, choose App+Enterprise Access.
   8. In the Application Scopes > Content Actions section, ensure you select the following checkbox options:
      1. Read all files and folders stored in Box.
      2. Write all files and folders stored in Box.
      3. Manage AI.
   9. Ensure you deselect all other checkbox options under Application Scopes > Administrative Actions and Application Scopes > Developer Actions.
   10. Click Save Changes.
   11. Back on the newly created app page, select Authorization > Review and Submit and then click Submit. Your new app will move to the Pending Authorization state.
2. Authorize the App in the Admin Console.
   1. Click Back to My Account on the left navigation pane and select Admin Console > Integrations > Platform Apps Manager.
   2. On the Server Authentication Apps list, find the app you created and select ... > Authorize App > Authorize.
3.  Retrieve the Enterprise ID

    1. Go Back to My Account > Dev Console and select the app you created.
    2. Copy the Enterprise ID (available in the General Settings tab).

    **Note**: Ensure you repeat the authorization process again if you modify any settings during configuration.
4. Onboard Box AI Agents to Cortex:
   1. Log in to Cortex.
   2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the Box connector.
   3. You may find multiple Box tiles, select the Box titled **Box integration for SaaS Data** and **Posture Security for Box**. Click on the tile and select the Add Another Instance.
   4. On the **Capabilities** page, provide an Instance Name and select the Agent Security scanning capability.
   5. On the **Connections** page, provide your Instance URL and select the Recommended authentication method. Provide your Client ID and Client Secret for the authentication flow.
   6. Once Cortex validates the credentials and permissions, the onboarding process is complete.
5. **Validation and Scanning**: Cortex validates the credentials and permissions. After the validation is successful, you will see a confirmation message. Scanning begins immediately after a successful validation. The amount of time Cortex takes to scan varies based on the amount of scan data. At a minimum, it takes at least one hour to scan and display data in the Cortex dashboard.
