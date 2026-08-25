---
description: >-
  Onboard Jamf Pro to Cortex XSIAM for SaaS security posture monitoring and
  compliance visibility.
---

# Onboard Jamf Pro

For SaaS Security to detect posture risks in your Jamf Pro instance, you must onboard your Jamf Pro instance to SaaS Security. Through the onboarding process, SaaS Security connects to the Jamf Pro API and, through the API, scans your Jamf Pro instance for misconfigured settings and account risks.

SaaS Security gets access to your Jamf Pro instance through an OAuth 2.0 client that you create. During onboarding, you supply SaaS Security with the application credentials (Client ID and Client Secret) for your OAuth 2.0 client. SaaS Security uses these credentials to access the Jamf Pro API through the OAuth 2.0 client.

To access your Jamf Pro instance, SaaS Security requires the following information, which you specify during the onboarding process.

| Item          | Description                                                                                                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Instance URL  | The unique URL for your Jamf Pro instance.                                                                                                                                                  |
| Client ID     | SaaS Security accesses the Jamf Pro API through an OAuth 2.0 client that you create in Jamf Pro. Jamf Pro generates the Client ID to uniquely identify this OAuth 2.0 client.               |
| Client Secret | SaaS Security accesses the Jamf Pro API through an OAuth 2.0 client that you create in Jamf Pro. Jamf Pro generates the Client Secret, which SaaS Security uses to authenticate to the API. |

To onboard your Jamf Pro instance, complete the following actions.

***

### Step 1: Identify Your Instance URL

Identify your instance URL, which appears in the browser's address bar. Jamf Pro typically creates your instance URL during the initial setup of your Jamf Pro environment. Your full instance URL has the format https://\<instance-name>.jamfcloud.com.

Before you continue to the next step, make note of this instance URL. You will provide this URL to SaaS Security during the onboarding process.

***

### Step 2: Create the OAuth 2.0 Client

An OAuth 2.0 client in Jamf Pro consists of one or more API roles and an API client. An API role is a custom privilege set designed for non-human API access. An API client is the non-human identity that SaaS Security uses to authenticate to your Jamf Pro instance.

Required Permissions: To create an API role and an API client, use an administrator account (an account assigned to the Administrator Privilege Set) with Full Access.

1. Identify the Jamf Pro account that you will use to create the OAuth 2.0 client.
2. Open a web browser to your Jamf Pro login page and log in to the administrator account you identified.
3. Create an API role to assign to your API client.

An API role defines a set of permissions for an API client. Create an API role that allows access to the scopes that SaaS Security needs to complete its scans.

1. From the left navigation pane, select Settings.
2. On the Settings page, locate the System settings and select API roles and clients.
3. On the API roles and clients page, select the API Roles tab and click + New.
4. On the New API Role page, complete the following actions:
5. Specify a Display name for the API role. For example, SaaS Security Role.
6. In the Privileges field, add the following privileges:

| Privileges                                                                                                                                                                                                   | Scan Type |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| Read Impact Alert Notification Settings, Read App Request Settings, Read Automatically Renew MDM Profile Settings, Read Policies, Read Re-enrollment, Read Computer Check-In, Read User-Initiated Enrollment | Posture   |
| Read API Integrations, Read API Roles, Read Accounts, Read Webhooks                                                                                                                                          | Identity  |

7. Click Save to save the API role.
8. Create the API client.

The API client is the Jamf Pro non-human identity that SaaS Security uses to authenticate with Jamf Pro. You assign the API role you created to this API client to limit the client's permissions. Creating the API client generates the Client ID and Client Secret necessary for the integration with SaaS Security.

1. On the API roles and clients page, select the API Clients tab and click + New.
2. On the New API Client page, complete the following actions:
3. Specify a Display name for the API client. For example, SaaS Security Integration.
4. In the API Roles field, add the API role that you created.
5. Click Enable API client.
6. Click Save. Jamf Pro saves the API client and displays its configuration details.
7. On the configuration details page for the API client, click Generate client secret. After you confirm that you want to create the secret, Jamf Pro generates and displays the application credentials (Client ID and Client Secret) for your API client.
8. Copy the credentials and paste them into a text file.

Note: Do not continue to the next step unless you have copied both the Client ID and Client Secret. You must provide these credentials to SaaS Security during the onboarding process.

***

### Step 3: Connect SaaS Security to Your Jamf Pro Instance

By adding a Jamf Pro app in Cortex, you enable SaaS Security to connect to your Jamf Pro instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Jamf Pro tile.
4. Under **Capabilities**, enter a name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter your instance URL and the application credentials (Client ID and Client Secret).
7. Under **Configurations**, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
