---
description: >-
  Connect a MongoDB Atlas instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard MongoDB Atlas

For SaaS Security to detect posture risks in your MongoDB Atlas instance, you must onboard your MongoDB Atlas instance to SaaS Security. Through the onboarding process, SaaS Security connects to the MongoDB Atlas Administration API by using programmatic credentials (Client ID and Client Secret) that you provide. After connecting to the MongoDB Atlas Administration API, SaaS Security scans your MongoDB Atlas organization for misconfigured settings and account risks.

To access your MongoDB Atlas instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item          | Description                                                                                                                                                                                                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client ID     | SaaS Security accesses the MongoDB Atlas Administration API through a MongoDB service account that you create. MongoDB Atlas generates a Client ID to uniquely identify the service account.                                                                                 |
| Client Secret | SaaS Security accesses the MongoDB Atlas Administration API through a MongoDB service account that you create. MongoDB Atlas generates a client secret for the service account. The API verifies the client secret against the client ID to confirm requests are legitimate. |

To onboard your MongoDB Atlas instance, complete the following actions.

***

### Step 1: Create a Service Account in MongoDB Atlas and Save Its Credentials

A MongoDB Atlas service account is a non-human, programmatic identity that SaaS Security uses to scan your MongoDB organization. When you create a service account, MongoDB Atlas generates and displays the programmatic credentials (Client ID and Client Secret) that SaaS Security uses to access information about your organization.

Note: By following these steps, you onboard only one MongoDB Atlas organization to SaaS Security. If you want SaaS Security to scan multiple organizations, onboard each organization separately.

1. Identify the MongoDB Atlas account that you will use to create the service account.

Required Permissions: A service account is scoped to one organization. To create a service account, you must be assigned to the Organization Owner role for the organization that you want SaaS Security to scan.

2. Open a web browser to [the MongoDB Atlas website](https://cloud.mongodb.com/) and log in to the Organization Owner account.
3. If you're a member of multiple organizations, make sure you're in the organization that you want SaaS Security to scan. A selection list in the top-left corner of the MongoDB Atlas page shows your current organization. If necessary, select a different organization from this list.
4. From the left navigation pane, select Access Manager.
5. On the Organization Access Manager page, select Add New > Service Account.
6. On the Create Service account page, specify the following information:

* A Name for the service account. For example, SaaS Security Service Account.
* A Description of the service account. For example, Service account for SaaS Security authentication.
* A Client Secret Expiration date. The recommended expiration period is 90 days.
* The Organization Permissions to grant to the service account. Select Organization Owner permissions. SaaS Security requires this level of access to complete its scans.

7. Click Create. MongoDB Atlas creates the service account and displays the programmatic credentials (Client ID and Client Secret) that SaaS Security uses for authentication.
8. Copy the Client ID and Client Secret and paste them into a text file.

**Note**: Do not continue to the next step unless you have copied the Client ID and Client Secret. You will provide this information to SaaS Security during the onboarding process.

***

### Step 2: Connect SaaS Security to Your MongoDB Atlas Instance

By adding a MongoDB Atlas app in Cortex, you enable SaaS Security to connect to your MongoDB Atlas instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the MongoDB Atlas tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter the Client ID and Client Secret.
7. Under **Configurations**, select a **Sync Interval.** Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.

<br>
