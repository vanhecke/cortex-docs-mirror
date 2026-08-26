---
description: >-
  Connect a Databricks instance in Cortex XSIAM to detect posture risks and
  compliance violations.
---

# Onboard Databricks

This page covers two onboarding methods. Use the method that matches your environment:

* [Onboard Using Credentials](https://docs.google.com/document/d/1EIc1VvKe4SEe6D7jGSeIc_PI5JdhlR6qPPcPrU8Mj70/edit#method-1-onboard-using-credentials-okta-or-azure-ad) — for posture scans using an administrator account via Okta or Azure AD
* [Onboard Using a Service Principal](https://docs.google.com/document/d/1EIc1VvKe4SEe6D7jGSeIc_PI5JdhlR6qPPcPrU8Mj70/edit#method-2-onboard-using-a-service-principal) — for identity scans using a Databricks managed service principal

***

### Method 1: Onboard Using Credentials (Okta or Azure AD)

For SaaS Security to detect posture risks in your Databricks instance, you must onboard your Databricks instance to SaaS Security. Through the onboarding process, SaaS Security logs in to Databricks using administrator account credentials via Okta SSO or Microsoft Azure AD.

To access your Databricks instance, SaaS Security requires the following information, which you specify during the onboarding process.

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

#### Step 1: Collect Credentials

1. Identify the account that SaaS Security will use to access your Databricks instance. The user account must have administrator privileges in Databricks.
2. Get a secret key for MFA. The steps differ depending on your identity provider:

* (For Okta login): Identify your Okta subdomain, then generate and copy an MFA secret key.
* (For Microsoft Azure login): Enable third-party software OATH tokens for the administrator account, then configure the account for MFA and copy the MFA secret key.

#### Step 2: Connect SaaS Security to Your Databricks Instance

By adding a Databricks app in Cortex, you enable SaaS Security to connect to your Databricks instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Databricks tile.
4. Enter a name for your app in the **Capabilities** field.
5. Select Security Posture under Security Capabilities.
6. Click Next.
7. On the **Connections** tab, specify how you want SaaS Security to connect: Log in with Okta or Log in with Azure.
8. When prompted, provide the login credentials and the information needed for MFA.
9. Click **Next** to complete the onboarding validation process.

***

### Method 2: Onboard Using a Service Principal

For SaaS Security to detect identity risks in your Databricks instance, you must onboard your Databricks instance to SaaS Security using a Databricks managed service principal. After connecting to the Databricks API, SaaS Security runs identity scans of your Databricks instance to detect account risks.

To onboard your Databricks instance, SaaS Security requires the following information.

| Item          | Description                                                                                                                                                                       |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client ID     | SaaS Security accesses a Databricks API through a service principal that you create. Databricks generates the Client ID to uniquely identify this service principal.              |
| Client Secret | SaaS Security accesses a Databricks API through a service principal that you create. Databricks generates the Client Secret, which SaaS Security uses to authenticate to the API. |
| Account ID    | An alphanumeric string that uniquely identifies your Databricks account.                                                                                                          |
| Warehouse ID  | The unique identifier of the SQL warehouse that SaaS Security will use to query data from your Databricks instance.                                                               |

Required Permissions: You must be assigned to both the Account Admin and Workspace Admin roles.

#### Step 1: Identify Your Account ID

1. Open a web browser to the [Databricks Account Console login page](https://accounts.cloud.databricks.com/login) and log in as an administrator assigned to both the Account Admin and Workspace Admin roles.
2. In the upper-right corner of the console, locate and click your user icon or name. The drop-down menu includes your account ID.
3. Copy your account ID and paste it into a text file.

Note: Do not continue to the next step unless you have copied the account ID. You will provide this information to SaaS Security during the onboarding process.

#### Step 2: Create a Databricks Managed Service Principal

A Databricks managed service principal is a non-human, programmatic identity that SaaS Security uses to scan your Databricks instance. When you create a service principal, Databricks generates and displays the Client ID and Client Secret that SaaS Security uses to access the Databricks API.

1. From the left navigation pane, select User management.
2. On the User Management page, select the Service principals tab and click Add service principal.
3. In the Add Service Principal dialog, specify a meaningful name for the service principal. For example: SaaS Security Service Principal. Click Add service principal to create it.

Databricks displays a configuration page for your new service principal.

4. On the configuration page, select the Roles tab and select the Account admin role.
5. Select the Credentials & Secrets tab and click Generate secret.
6. In the Generate OAuth Secret dialog, specify an expiration period and click Generate.

Databricks displays the Client ID and Client Secret for your service principal.

7. Copy the Client ID and Client Secret and paste them into a text file.

Note: Do not continue to the next step unless you have copied the Client ID and Client Secret. You will provide this information to SaaS Security during the onboarding process.

#### Step 3: Create an SQL Warehouse

Note: If you already have an SQL warehouse, skip this step and provide its warehouse ID to SaaS Security during onboarding. It is not necessary to create a warehouse exclusively for SaaS Security.

The SQL warehouse provides SaaS Security with the compute resources needed to run SQL queries on your Databricks instance.

1. Navigate to a workspace where you will create the SQL warehouse:

* From the left navigation pane, select Workspaces.
* On the Workspaces page, click the link for the workspace.
* On the workspace's page, click the URL link.

Note: If you have multiple workspaces, create the SQL warehouse in any one of them. Because all workspaces are linked to a central Unity Catalog metastore, the warehouse can query data across workspaces.

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

#### Step 4: Enable Delta Sharing for Your Databricks Workspaces

Repeat the following steps for each of your workspaces:

1. From the left navigation pane, select Workspaces.
2. On the Workspaces page, click the link for the workspace's Metastore.
3. On the Configuration tab for the metastore, select the check box to Allow Delta Sharing with parties outside your organization.

#### Step 5: Connect SaaS Security to Your Databricks Instance

By adding a Databricks app in Cortex, you enable SaaS Security to connect to your Databricks instance.

1. Log in to Cortex.
2. Select **Settings > Data Sources and Integrations > Add New**. You can use the Search bar to find the app you want to connect to.
3. Click the Databricks tile.
4. Under **Capabilities**, Enter a Name for your application.
5. Select Security Posture under Default Capabilities and click Next.
6. Under **Connections**, enter the Client ID, Client Secret, Account ID, and Warehouse ID.
7. Under **Configurations**, select a Sync Interval. Choose a meaningful Tag to distinguish between various applications in different environments.
8. Click **Next** to complete the onboarding validation process.
