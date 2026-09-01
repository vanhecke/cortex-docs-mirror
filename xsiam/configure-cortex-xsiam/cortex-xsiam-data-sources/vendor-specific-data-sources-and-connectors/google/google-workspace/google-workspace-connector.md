---
description: Use Google Workspace with Cortex XSIAM.
---

# Google Workspace connector

Secure sensitive data, monitor identity risks, and ensure compliance across your Google Workspace environment.

This connector includes the following capabilities and sub-capabilities (if applicable):

* **Automation and Remediation:** Run automation and remediation actions against Google Drive. This capability is available with any active Cortex AgentiX or Cortex XSIAM license.
* **Data Security:** Scan and protect Google Workspace data across Drive, Gmail, and shared resources. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
* **Identity Posture:** Maintain visibility and control over Google Workspace identities, including users, groups, roles, and privileges. This capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Groups:** Ingest user groups from Google Workspace. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Privileges:** Ingest privileges from Google Workspace. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Roles:** Ingest roles from Google Workspace. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.
  * **Users:** Ingest users from Google Workspace. This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.

To configure this connector, follow these steps:

#### Prerequisites

Create a service account and generate a JSON key in the Google Cloud Console. Cortex Cloud uses this service account to authenticate and access Google Workspace resources.

#### 1. Enable the Google Drive API

1. Sign in to the Google Cloud Console with an account that has the following administrative privileges: Users → user → Admin Roles and privileges → Role=Super Admin.
2. From the project selector, select an existing project or create a new project.
3. Go to **APIs & Services** > **Library**.
4. Search for **Google Drive API**.
5. Select **Google Drive API**, and click **Enable**.

#### 2. Create a Service Account and Generate a JSON Key

1. Log in to [`https://console.cloud.google.com/`](https://console.cloud.google.com/) using the super admin user credentials.
2. Go to **APIs & Services** > **Credentials**.
3. Click **Create Credentials**, and select **Service Account**.
4.  Enter a descriptive name for the service account.

    **Note:** The **Service account ID** is generated automatically based on the service account name.
5. Click **Create and Continue**, and then click **Done**.
6. Locate the newly created **service account** and open its details.
7. Select the **Keys** tab.
8. Select **Add Key** > **Create new key**.
9. Select **JSON**, and click **Create**.
10. Copy the **Client Id** and download the generated JSON key file and securely store it on your local machine.
11. Navigate to **APIs & Services** -> **Enabled APIs & services**.
12. Click **+ Enable APIs and services**.&#x20;
13. Search for **Admin SDK API** and enable it.

#### 3. Configure Domain wide Delegation permissions

1. Navigate to [`https://admin.google.com/`](https://admin.google.com/).
2. Navigate to **Security** -> **Access and data control** -> **API controls**.
3. Click on **MANAGE DOMAIN WIDE DELEGATION**.
4. Click on **Add new**.
5. Provide the new **Service Account UniqueId** created above, add all the below scopes, and click **AUTHORIZE**:
   1.  Scopes required by Identity and Data Security:

       [`https://www.googleapis.com/auth/admin.directory.customer.readonly`](https://www.googleapis.com/auth/admin.directory.customer.readonly)[`https://www.googleapis.com/auth/admin.directory.user.readonly`](https://www.googleapis.com/auth/admin.directory.user.readonly)[`https://www.googleapis.com/auth/admin.directory.group.readonly`](https://www.googleapis.com/auth/admin.directory.group.readonly)[`https://www.googleapis.com/auth/admin.directory.group.member.readonly`](https://www.googleapis.com/auth/admin.directory.group.member.readonly)[`https://www.googleapis.com/auth/admin.directory.rolemanagement.readonly`](https://www.googleapis.com/auth/admin.directory.rolemanagement.readonly)

       [`https://www.googleapis.com/auth/drive`](https://www.googleapis.com/auth/drive)[`https://www.googleapis.com/auth/admin.directory.user.readonly`](https://www.googleapis.com/auth/admin.directory.user.readonly)
   2.  Scopes required by Logs Ingestion:

       [`https://www.googleapis.com/auth/admin.reports.audit.readonly`](https://www.googleapis.com/auth/admin.reports.audit.readonly)[`https://www.googleapis.com/auth/admin.reports.usage.readonly`](https://www.googleapis.com/auth/admin.reports.usage.readonly)

#### 4. Configure the Google Workspace logs and data Ingestion

Before configuring Google Workspace, enable the Google Workspace logs ingestion to collect the Management Activity logs required for workspace scanning.

For detailed configuration steps, see [Configure the Google workspace logs ingestion](ingest-logs-and-data-from-google-workspace).

### How to configure the Google Workspace connector

#### Task 1. Select services

1. In Cortex Cloud, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. On the **Add Data Source** page, search for **Google Workspace**, hover over it, and click **Add**.

#### Capabilities tab

1. Enter a unique name for the new connector instance.
2. Select **Data Security** and **Identity Posture**.
3. Click **Next**.

#### Connection tab

1. On the **Connection** tab, locate the **Google Workspace Admin Email** field.
2. Enter your Google Workspace administrator email address.
3. Click **Apply**.
4. Upload the JSON credentials file that you generated earlier.
5. Click **Test** to validate the connection.
6. If the connection is successful, the status displays a green **Verified** indicator.
7. Click **Next**.

#### Summary tab

1. On the **Summary** tab, verify that all selected capabilities display a **Connected** status.
2. If validation succeeds, the wizard displays a **Verification Success** message.
3. Click **Create Instance** to create the Google Workspace connector.

#### Task 2. (Optional) Post verification

After the configuration is complete, verify asset discovery and data security findings.

#### 1. Verify Discovered Assets

1. Go to **Inventory** > **All Assets**.
2. Filter the asset list by setting **Provider** to **Google Workspace**.
3. Verify that Cortex discovers the following supported asset types:
   * **Google Personal Drive:** Individual user drives that contain personal files, documents, and private folder structures.
   * **Google Shared Drive:** Organization-owned shared drives used to store collaborative documents and project content.

#### 2. Verify Security and Policy Findings

1. Select an asset to open its details panel.
2. Click the **Overview** tab to review general metadata, file counts, and finding details.
3. Go to **Findings** to review detected security findings, including:
   * **Sensitive Data Exposure:** PII, credit card numbers (PCI), Social Security numbers (SSNs), or proprietary source code detected in Google Docs, Sheets, Slides, or PDF attachments.
   * **External and Public Sharing Risks:** Files shared publicly through links, such as **Anyone with the link**, or files shared with external third-party email domains.
   * **Orphaned or Unowned File Risks:** Files owned by deleted or suspended user accounts.
