---
description: >-
  Connect ServiceNow in Cortex XSIAM SaaS Agent Security for visibility and
  control across your AI ecosystem.
---

# Onboard Service Now

To secure access to your ServiceNow data and successfully onboard to Cortex, you must complete two main phases:

1. Create an application registry that the platform will use to access your ServiceNow data via the REST API. The configuration consists of creating a user, creating an authentication scope, and using them to create an application registry.
2. Onboard the ServiceNow platform to AISPM via Strata Cloud Manager.

**Prerequisites**: Ensure you have the necessary administrative privileges in your ServiceNow instance, including the ability to elevate your role to security\_admin to create and manage Access Control Lists (ACLs).

### Create an Application Registry

1. Create a Service User\
   Note: Ensure you elevate your role to security\_admin before creating the user and grant read-only access to the required tables using Access Control Lists (ACLs). You could also edit existing roles.
   1. Sign in to your ServiceNow instance.
   2. In the search box, start typing and select User Administration > Users > New and enter the following details:
      1. User ID
      2. First name and Last name
      3. Email
   3. Select the Web service access only check box. (Note: This is critical as it ensures the user cannot be used for interactive sign-in.)
   4. Select the Active check box and Submit the new user record.
   5. Select a role for the new user:
      * The role must have read and write permission to the sys\_gen\_ai\_skill\_applicability table.
      * For all other tables, only read permission is required.
      * If necessary, you can create a custom role in ServiceNow with these specific permissions. The read permission will enable AISPM to scan the ServiceNow AI Platform for agent risks. The write permission to the applicability table will enable you to remediate risky plugins and take agents offline.
2.  Create the Authentication Scope\
    Note: Before creating the OAuth 2.0 integration, create a scope that limits AISPM's access to only the Table API.

    1. Navigate to the Authentication Scopes table (sys\_auth\_scope.list) by using the filter navigator.
    2. Click New to define the authentication scope.
    3. Specify a meaningful Name for your authentication scope, such as SaaS\_Agent\_Security\_Scope or SSPM Agentic Scope.
    4. (Optional) Specify a Description. Click Submit.

    Note: Keep the authentication scope name handy, as it is required when configuring the REST API Auth Scope and OAuth 2.0 integration.
3. Create the Application Registry (OAuth Client)\
   Standard Release Instructions:
   1. Log in to ServiceNow as an administrator.
   2. Navigate to the Application Registries page (System OAuth > Application Registry).
   3. Select New > Create an OAuth API endpoint for external clients.
   4. Copy the auto-generated Client ID and Client Secret and keep them handy.
   5. Ensure the following additional details are filled in correctly:
   6. Set the Application to Global.
   7. Ensure it's accessible from all application scopes.
   8. Ensure the Active check box is selected.
   9. OAuth Application User: Enter the user you created in Step 1.
   10. Default grant type: Choose Client Credentials. (Ensure that the system property glide.oauth.inbound.client.credential.grant\_type.enabled is set to true).
   11. Specify your OAuth Scope that you created in Step 2.
   12. Click Submit.
4. Onboard ServiceNow Platform to Cortex.
   1. Log in to Cortex.
   2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the ServiceNow connector.
   3. Click on the ServiceNow tile and select Add Another Instance.
   4. On the **Capabilities** page, provide an Instance Name and select Agent Security scanning capability.
   5. On the **Connections** page, provide your Instance URL and select an authentication method. Enter the information you gathered (Client ID, Client Secret, etc.) during Step 1 in the corresponding fields.
   6. Once AISPM validates the credentials and permissions, the onboarding process is complete.

#### Troubleshooting

If you see errors after onboarding, this is likely due to incomplete permissions. Return to the application registry creation procedure and verify that the assigned role possesses a read-only ACL rule for every single required table. Also, ensure that this role is correctly assigned to the service user you created.
