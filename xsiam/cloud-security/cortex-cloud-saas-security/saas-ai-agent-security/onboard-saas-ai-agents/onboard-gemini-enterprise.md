---
description: >-
  Connect Gemini Enterprise in Cortex XSIAM SaaS Agent Security for visibility
  and control across your AI ecosystem.
---

# Onboard Gemini Enterprise

Gemini allows employees to use pre-built agents or create their own custom agents to perform tasks, analyze data, and automate workflows by securely connecting to company data and applications like Google Workspace and Salesforce. The platform aims to shift employees from tedious tasks to high-impact work while providing central governance and security.

To access your Gemini Enterprise instance, AISPM requires the following specific information during the configuration process:

| Item                  | Description                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Service Account Email | A service account email in Gemini Enterprise is a special non-human account. Applications and virtual machines use this account to authenticate and access Google Cloud resources securely. It provides a secure identity for programmatic access to the Gemini for Google Cloud API and related services.                                                                                                   |
| Project ID            | A Project ID in Gemini Enterprise is a unique identifier for a Google Cloud project. Gemini Enterprise uses the Google Cloud platform, so its services and resources are organized within the same project structure. A Project ID is needed for authentication, billing, and access control when working with Gemini models and related services.                                                           |
| Location              | <p>In Google Cloud's Gemini Enterprise, a "location" is a specific geographic area for creating, processing, and storing data. Location selection allows enterprises to control data residency. This control is important for data privacy, compliance, and meeting requirements in different regions.</p><p>Note: New locations created by Gemini Enterprise will be added by AISPM in a phased manner.</p> |

1. Configure Google Cloud Console.
   1. Go to your project home page (where you developed your agent) in the Google Cloud console. Copy your project ID and project number and keep it handy for onboarding later.
   2. From the Google Cloud console, select Menu > APIs & Services > Enabled APIs & Services > +Enable APIs and services.
   3. To create a new service account, select Menu > IAM & Admin > Service Accounts > +Create service account.
   4. In the list of service accounts, click on the service account that you just created. The service account details are displayed. Copy the service account email address and keep it handy for onboarding later.
   5. Select Principals with access > View by principals > Grant access.
   6. In the Add principals section, specify the name of the principal.
   7. In the Assign roles section, select the Service Account Token Creator role and click Save.
2. Onboard Platform to AISPM
   1. Log in to Cortex.
   2. Select Settings > Data Sources and Integrations > Add New. You can use the Search bar to find the Gemini Enterprise connector.
   3. Click on the Gemini Enterprise tile and select Add Another Instance.
   4. On the Capabilities page, provide an Instance Name and select Agent Security scanning capability.
   5. On the Connections page enter the following information that you gathered in Step 1:
      1. Project ID (You can use either the project ID or the project number.)
      2. Service Account Email
   6. Once AISPM validates the credentials and permissions, the onboarding process is complete.
3. Validation and Scanning: Cortex establishes the API connection and validates the credentials and permissions. Cortex immediately begins to scan your onboarded agentic platform after a successful validation. The amount of time Cortex takes to scan varies based on the amount of data it is required to scan. At a minimum, it takes at least one hour to scan and display data in the AISPM dashboard.
