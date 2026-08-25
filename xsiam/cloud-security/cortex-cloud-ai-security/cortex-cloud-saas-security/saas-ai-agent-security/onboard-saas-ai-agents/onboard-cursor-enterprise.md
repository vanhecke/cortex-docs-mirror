---
description: >-
  Onboard Cursor Enterprise to Cortex XSIAM SaaS AI Agent Security for
  visibility and control.
---

# Onboard Cursor Enterprise

Cursor Enterprise is the secure, scalable version of Cursor, an AI-powered code editor built on VS Code. It is designed for large organizations needing advanced features like SSO, audit logs, usage analytics, and data privacy controls to manage AI-assisted software development for complex codebases. It provides features such as IP allowlisting, team management, centralized security, and compliance tools (GDPR, CCPA, SOC 2) to meet enterprise security and governance needs, allowing teams to build faster and more efficiently.

**Important**: Due to Cursor Enterprise API restrictions, any discovery for Tools and Knowledge Bases is limited to the last 30 days. If you want to increase this duration, contact Technical Support.

1. Create an Admin API Key in Cursor Enterprise.
   1. Go to the Cursor Enterprise dashboard and select Settings > API Keys > New API Key.
   2. Copy the generated Admin API Key and keep it handy for the onboarding steps.
2. Onboard Cursor Enterprise to Cortex.
   1. Log in to Cortex.
   2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the Cursor connector.
   3. Click on the Cursor tile and select **Add Another Instance**.
   4. On the **Capabilities** page, provide an Instance Name and select Agent Security scanning capability.
   5. On the **Connections** page, provide your Instance URL and enter your API Key to initiate the authentication flow.
   6. Once AISPM validates the credentials and permissions, the onboarding process is complete.
3. Validation and Scanning: Cortex establishes the connection and validates the credentials and permissions. After successful validation, you will see a confirmation message. The amount of time Cortex takes to scan varies based on the amount of data it is required to scan. At a minimum, it takes at least one hour to scan and display data in the AISPM dashboard.
