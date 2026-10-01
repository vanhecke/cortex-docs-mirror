---
description: Use Databricks data with Cortex XSIAM.
---

# Databricks

Secure configurations and monitor identity risks across your Databricks environment.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Identity Posture:** Maintain visibility and control over Databricks identities, including users, groups, roles, and service principals. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Groups:** Ingest user groups from Databricks. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Roles:** Ingest roles from Databricks. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Service Principals:** Ingest service principals from Databricks. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Users:** Ingest users from Databricks. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Security Posture:** Detect, monitor and alert on settings of your SaaS application. This capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.
  * **saas-posture-config-remediation:** Help remediate the misconfigured security settings of your SaaS application. This sub-capability is available with any active Cortex XSIAM or Cortex Cloud Posture Security license.

<details>

<summary><strong>Security Posture</strong></summary>

This page covers two onboarding methods. Use the method that matches your environment:

* [Onboard Using Credentials](#method-1-onboard-using-credentials-okta-or-azure-ad) — for posture scans using an administrator account via Okta or Azure AD
* [Onboard Using a Service Principal](#method-2-onboard-using-a-service-principal) — for identity scans using a Databricks managed service principal

***

### Method 1: Onboard Using Credentials (Okta or Azure AD)

To access your Databricks instance, Cortex XSIAM requires the following information, which you specify during the onboarding process.

| Item     | Description                                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Username | The username or email address of the account that SaaS Security will use to access your Databricks instance. Required Permissions: The user must be a Databricks administrator. |
| Password | The password for the login account.                                                                                                                                             |

If you're logging in through Okta, you must also provide:

| Item            | Description                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| Okta subdomain  | The Okta subdomain for your organization, included in the login URL that Okta assigned to your organization. |
| Okta 2FA secret | A key used to generate one-time passcodes for MFA.                                                           |

If you're using Azure Active Directory (AD) as your identity provider, you must also provide:

| Item             | Description                                        |
| ---------------- | -------------------------------------------------- |
| Azure 2FA secret | A key used to generate one-time passcodes for MFA. |

#### Task 1: Collect Credentials

1. Identify the account that Cortex XSIAM will use to access your Databricks instance. The user account must have administrator privileges in Databricks.
2. Get a secret key for MFA. The steps differ depending on your identity provider:

* (For Okta login): Identify your Okta subdomain, then generate and copy an MFA secret key.
* (For Microsoft Azure login): Enable third-party software OAuth tokens for the administrator account, then configure the account for MFA and copy the MFA secret key.

#### Task 2: Connect Cortex XSIAM to Your Databricks Instance

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Databricks.
4. Under **Recommended**, hover over the new Databricks integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. On the **Connections** tab, specify how you want Cortex XSIAM to connect: Log in with Okta or Log in with Azure.
9. When prompted, provide the login credentials and the information needed for MFA.
10. A confirmation message indicates that Databricks is successfully connected. Confirm the Summary details and click **Save instance**.

***

### Method 2: Onboard Using a Service Principal

To onboard your Databricks instance, Cortex XSIAM requires the following information.

| Item          | Description                                                                                                                                                                      |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client ID     | Cortex XSIAM accesses a Databricks API through a service principal that you create. Databricks generates the Client ID to uniquely identify this service principal.              |
| Client Secret | Cortex XSIAM accesses a Databricks API through a service principal that you create. Databricks generates the Client Secret, which SaaS Security uses to authenticate to the API. |
| Account ID    | An alphanumeric string that uniquely identifies your Databricks account.                                                                                                         |
| Warehouse ID  | The unique identifier of the SQL warehouse that SaaS Security will use to query data from your Databricks instance.                                                              |

Required Permissions: You must be assigned to both the Account Admin and Workspace Admin roles.

#### Task 1: Identify Your Account ID

1. Open a web browser to the [Databricks Account Console login page](https://accounts.cloud.databricks.com/login) and log in as an administrator assigned to both the Account Admin and Workspace Admin roles.
2. In the upper-right corner of the console, locate and click your user icon or name. The drop-down menu includes your account ID.
3. Copy your account ID and paste it into a text file.

{% hint style="info" %}
Do not continue to the next step unless you have copied the account ID. You will provide this information to SaaS Security during the onboarding process.
{% endhint %}

#### Task 2: Create a Databricks Managed Service Principal

A Databricks managed service principal is a non-human, programmatic identity that SaaS Security uses to scan your Databricks instance. When you create a service principal, Databricks generates and displays the Client ID and Client Secret that SaaS Security uses to access the Databricks API.

1. From the left navigation pane, select User management.
2. On the User Management page, select the Service principals tab and click Add service principal.
3. In the Add Service Principal dialog, specify a meaningful name for the service principal. For example: SaaS Security Service Principal. Click Add service principal to create it.

Databricks displays a configuration page for your new service principal.

4. On the configuration page, select the Roles tab and select the Account admin role.
5. Select the Credentials & Secrets tab and click Generate secret.
6. In the Generate OAuth Secret dialog, specify an expiration period and click Generate.

Databricks displays the Client ID and Client Secret for your service principal.

7. Copy the Client ID and Client Secret and paste them into a text file. Do not continue to the next step unless you have copied the Client ID and Client Secret. You will provide this information to SaaS Security during the onboarding process.

#### Task 3: Create an SQL Warehouse

If you already have an SQL warehouse, skip this step and provide its warehouse ID to SaaS Security during onboarding. It is not necessary to create a warehouse exclusively for SaaS Security.

The SQL warehouse provides SaaS Security with the compute resources needed to run SQL queries on your Databricks instance.

1. Navigate to a workspace where you will create the SQL warehouse:

* From the left navigation pane, select Workspaces.
* On the Workspaces page, click the link for the workspace.
* On the workspace's page, click the URL link.

If you have multiple workspaces, create the SQL warehouse in any one of them. Because all workspaces are linked to a central Unity Catalog Metastore, the warehouse can query data across workspaces.

2. From the left navigation pane, select SQL Warehouses. Databricks opens the Compute page at the SQL Warehouses tab.
3. Click Create SQL Warehouse.
4.  In the New SQL Warehouse dialog:

    1. Specify a Name for the warehouse. For example, SaaS Security Warehouse.
    2. Specify a Cluster size. The minimum requirement is 2X-Small.
    3. Set the Auto stop time to 5 minutes.
    4. Click Create. Databricks creates the SQL warehouse and displays an Overview of its properties.
    5. From the overview page, copy the warehouse ID and paste it into a text file.

    Note: Do not continue to the next step unless you have copied the warehouse ID. You will provide this information to SaaS Security during the onboarding process.
5. Grant your service principal permission to execute queries on the warehouse:
6. From the overview page, select Permissions.
7. Use the search field in the Manage Permissions dialog to select the service principal.
8. Set the service principal's permission to Can use.
9. From the overview page, click Start to start the warehouse.

#### Task 4: Enable Delta Sharing for Your Databricks Workspaces

Repeat the following steps for each of your workspaces:

1. From the left navigation pane, select Workspaces.
2. On the Workspaces page, click the link for the workspace's Metastore.
3. On the Configuration tab for the Metastore, select the check box to Allow Delta Sharing with parties outside your organization.

#### Task 5: Connect Cortex XSIAM to Your Databricks Instance

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for Databricks.
4. Under **Recommended**, hover over the new Databricks integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connections**, enter the Client ID, Client Secret, Account ID, and Warehouse ID.
9. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
10. A confirmation message indicates that Databricks is successfully connected. Confirm the Summary details and click **Save instance**.

</details>
