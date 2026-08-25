---
description: >-
  Onboard ChatGPT Enterprise to Cortex XSIAM SaaS AI Agent Security for
  visibility and control.
---

# Onboard ChatGPT Enterprise

1. ChatGPT Enterprise & OpenAI Configuration
   1. Sign in to your ChatGPT Enterprise instance.
   2. Fetch the Organization ID and Workspace ID from ChatGPT Settings:
      1. Select ChatGPT > Manage Workspace > Settings and keep them handy.
   3. To fetch the Secret Key, go to the OpenAI API-Keys site and click + Create new secret key.
      1. In the Create new secret key page, enter the required details and click Create secret key.
      2. During key generation, ensure that the Permissions is set to All. (OpenAI will revoke it in the subsequent steps).
   4. Ensure that this key is generated in the same Organization as your ChatGPT tenant. To confirm this, select Settings on the OpenAI website and ensure the Org ID is the same as what you fetched previously.
   5. Copy the new key and keep it handy.
   6.  To enable the generated key for the Compliance API scopes, send an email to support@openai.com with the following information:

       1. Last 4 characters of the generated API Key
       2. Key Name
       3. Created By Name
       4. Requested Scope - Read. Ensure that the generated key is unique for AISPM and not used in any other product. For example, you cannot use the same key for both Data Security and AISPM since the scope is different for both of them.
       5. Organization ID

       **Note**: Further instructions are available in the ChatGPT API Reference.
2. After OpenAI enables the key for the Compliance API, proceed to add the ChatGPT Enterprise connector.
3. Onboarding ChatGPT to Cortex:
   1. Log in to Cortex.
   2. Select **Settings > Data Sources and Integrations > Add New.** You can use the Search bar to find the ChatGPT connector.
   3. Click on the ChatGPT tile and select the **Add Another Instance**.
   4. On the **Capabilities** page, provide an Instance Name and select Agent Security scanning capability.
   5. On the **Connections** page, provide your Instance URL and select the Recommended authentication method, enter the following information (that you gathered in the steps above and click Complete:
      1. Organization ID
      2. Workspace ID
      3. API Key
   6. Once Cortex validates the credentials and permissions, the onboarding process is complete.
4. Validation and Scanning: Cortex establishes the API connection and validates the credentials and permissions. After the validation is successful, you will see a confirmation message. Scan periods vary based on the amount of data it is required to scan. At a minimum, it takes at least one hour to scan and display data in the AISPM dashboard.
