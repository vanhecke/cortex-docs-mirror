---
description: >-
  Connect Microsoft Copilot Studio to SaaS Agent Security to gain total
  visibility and control over your AI ecosystem.
---

# Onboard Microsoft Copilot Studio

**Prerequisites**

* Licensing: To access Microsoft Copilot Studio and start building custom agents, your organization must have an active Microsoft Copilot Studio license. Coordinate with your IT Administrator or Microsoft Sales representative to ensure the proper licensing is in place. Note: Copilot Studio is a Microsoft-native product, not a feature developed or managed by Palo Alto Networks.
* Azure Permissions: Ensure you have Administrative privileges in the Microsoft Azure portal to register apps and grant API permissions. To perform onboarding, you must have an Application Administrator role. This role manages application settings and permissions within Microsoft Entra ID (Azure AD) and has the ability to restart provisioning of an enterprise application.
* Power Platform Permissions: Ensure you have a System Administrator or Power Platform Administrator role to add app users to the relevant environment.
* Environment Settings: Ensure you disable Administration mode in the Power Platform Admin Center.



1. Configure Permissions in Microsoft Azure.&#x20;

Create an app registration in your Microsoft Azure Portal to grant Palo Alto Networks® secure, read-only access to your Microsoft Copilot Studio environment.

1. Register a new app in Microsoft Azure
   1. Log in to the Microsoft Azure Portal.
   2. Navigate to or search for App registrations.
   3. Click + New Registration.
   4. Enter a descriptive Name for the app (for example: PaloAltoNetworks\_Agent\_Security\_Connector).
   5. Click Register.
2. Configure API permissions for the new app
   1. From the new app details page, select Manage > API permissions.
   2. Click + Add a permission and select Application permissions under Microsoft Graph.
   3. Add the following Microsoft Graph permissions:
      1. Application.Read.All
      2. AuditLog.Read.All
      3. AuditLogsQuery-CRM.Read.All
      4. AuditLogsQuery.Read.All
   4. Click Add permissions to save the app API permissions.
   5. Grant Admin Consent: The permissions you added require admin consent. On the Configured permissions page, click Grant admin consent for \<your-organization>.
   6. In the confirmation pop-up, select Yes to grant admin consent for your organization.
3. Create a Client Secret for the new app
   1. From the new app details page, select Manage > Certificates & secrets.
   2. Click + New client secret.
   3. Enter a description (for example: SaaS\_Security\_Key) and select an expiration period.
   4. Click Add.
   5. CRITICAL: Copy the Client Secret Value immediately and store it in a secure location. This value will be hidden permanently once you leave the page.
   6. Grant the app access in the Microsoft Power Platform admin center
4. Log in to the Microsoft Power Platform Admin Center.
   1. Select Manage > Environments and click on your target Copilot Studio environment.
   2. Navigate to Settings > Users + permissions > Application users and click + New app user.
   3. Click + Add an app and search for the application registration you created in Step 1.
   4. Select the correct Business unit from the drop-down menu.
   5. Click the pencil icon next to Security roles, assign the Service Reader role, and click Save.
   6. Click Create to finalize the app access privileges.
5. Gather the required configuration values
   1. Before moving to the next step, ensure you have gathered and copied the following variables:
      1. Environment URL: Found on the environment's main page in the Microsoft Power Platform Admin Center.
      2. Application (Client) ID: Displayed in the app Overview tab in the Microsoft Azure Portal.
      3. Directory (Tenant) ID: Displayed in the app Overview tab in the Microsoft Azure Portal.
      4. Client Secret Value: The secret value you securely stored in Step 3.
6. Onboard Microsoft Copilot Studio to AISPM. Establish the API connection between the Palo Alto Networks platform and your Microsoft Copilot Studio environment using the gathered credentials.
   1. Log in to Cortex.&#x20;
   2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the Microsoft Copilot Studio connector.
   3. Click on the Microsoft Copilot Studio tile and select **Add Another Instance**.&#x20;
      1. On the **Capabilities** page, provide an Instance Name and select Agent Security scanning capability.
   4. On the **Connections** page, provide your Instance URL and select an authentication method. Input the following:
      1. Tenant ID
         1. Power Platform Environment URL
   5. Under **Agent Security Scanning**, provide the Client ID and Client Secret.
   6. Once AISPM validates the credentials and permissions, the onboarding process is complete.
7. Validation and Scanning: Cortex will process the credentials and notify you once onboarding is complete. The amount of time required to complete the scan varies depending on your tenant's total volume of data. At a minimum, expect it to take at least one hour to process logs and display security telemetry inside the AISPM dashboard.

### Troubleshooting Potential Onboarding Failures

If Microsoft Copilot Studio fails to onboard, AISPM will flag one of the following error states:

* Permission Errors during Scan: Verify you entered all credentials correctly and double-check that you successfully executed the Grant Admin Consent step when configuring your Azure API Permissions.
* Connection Test Fails: Confirm that you assigned the Service Reader role to the application user inside the Power Platform Admin Center.
