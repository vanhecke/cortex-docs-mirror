---
description: Use Jamf Pro data with Cortex XSIAM.
---

# Jamf Pro

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Security Posture: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

### How to configure the Jamf Pro connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access Jamf Pro, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Instance URL**: The unique URL for your Jamf Pro instance.
* **Client ID**: Cortex XSIAM accesses the Jamf Pro API through an OAuth 2.0 client that you create in Jamf Pro. Jamf Pro generates the Client ID to uniquely identify this OAuth 2.0 client.
* **Client Secret**: Cortex XSIAM accesses the Jamf Pro API through an OAuth 2.0 client that you create in Jamf Pro. Jamf Pro generates the Client Secret, which Cortex XSIAM uses to authenticate to the API.

#### **Task 1:** Identify your instance URL

Identify your instance URL, which appears in the browser's address bar. Jamf Pro typically creates your instance URL during the initial setup of your environment. Your full instance URL has the format https://\<instance-name>.jamfcloud.com.

Before you continue to the next step, make note of this instance URL. You will provide this URL to Cortex XSIAM during the onboarding process.

#### Task 2: Create the OAuth 2.0 client <a href="#step-2-create-the-oauth-2.0-client" id="step-2-create-the-oauth-2.0-client"></a>

An OAuth 2.0 client in Jamf Pro consists of one or more API roles and an API client. An API role is a custom privilege set designed for non-human API access. An API client is the non-human identity that Cortex XSIAM uses to authenticate to your Jamf Pro instance.

Required Permissions: To create an API role and an API client, use an administrator account (an account assigned to the Administrator Privilege Set) with Full Access.

1. Identify the Jamf Pro account that you will use to create the OAuth 2.0 client.
2. Open a web browser to your Jamf Pro login page and log in to the administrator account you identified.
3. Create an API role to assign to your API client.

An API role defines a set of permissions for an API client. Create an API role that allows access to the scopes that Cortex XSIAM needs to complete its scans.

1. From the left navigation pane, select **Settings**.
2. On the Settings page, locate the System settings and select API roles and clients.
3. On the API roles and clients page, select the API Roles tab and click **+ New**.
4. On the New API Role page, complete the following actions:
5. Specify a Display name for the API role. For example, SaaS Security Role.
6. In the Privileges field, add the following privileges:

| Privileges                                                                                                                                                                                                   | Scan Type |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| Read Impact Alert Notification Settings, Read App Request Settings, Read Automatically Renew MDM Profile Settings, Read Policies, Read Re-enrollment, Read Computer Check-In, Read User-Initiated Enrollment | Posture   |
| Read API Integrations, Read API Roles, Read Accounts, Read Webhooks                                                                                                                                          | Identity  |

7. Click **Save** to save the API role.
8. Create the API client. The API client is the Jamf Pro non-human identity that Cortex XSIAM uses to authenticate with Jamf Pro. You assign the API role you created to this API client to limit the client's permissions. Creating the API client generates the Client ID and Client Secret necessary for the integration with Cortex XSIAM.
9. On the API roles and clients page, select the API Clients tab and click **+ New**.
10. On the New API Client page, complete the following actions:
    1. Specify a Display name for the API client. For example, SaaS Security Integration.
    2. In the API Roles field, add the API role that you created.
    3. Click **Enable API client**.
    4. Click **Save**. Jamf Pro saves the API client and displays its configuration details.
11. On the configuration details page for the API client, click **Generate client secret**. After you confirm that you want to create the secret, Jamf Pro generates and displays the application credentials (Client ID and Client Secret) for your API client.
12. Copy the credentials and paste them into a text file. Do not continue to the next step unless you have copied both the Client ID and Client Secret. You must provide these credentials to Cortex XSIAM during the onboarding process.

#### **Task 3: Connect** Jamf Pro **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Jamf Pro.
4. Under **Recommended**, hover over the new Jamf Pro integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter your instance URL and the application credentials (Client ID and Client Secret).
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that Jamf Pro is successfully connected. Confirm the Summary details and click **Save instance**.
