---
description: Connect Google Workspace to Cortex XSIAM through your GCP instance.
---

# Connect Google Workspace with your GCP cloud instance

To gain full visibility into GCP permissions and identity relationships, highlight risks, and offer proper remediation, Cortex XSIAM must ingest user, group, and group membership data from your Google Workspace. You need to create a custom role in Google Workspace, assign it specific privileges, and then assign your Cortex XSIAM service account to this newly created role.

{% hint style="info" %}
Prerequisite

Ensure you have the Super Admin role in Google Workspace.
{% endhint %}

### 1. Create a Cortex XSIAM role in Google Workspace

1. Log in to your [Google Admin Console](https://admin.google.com/).
2. In the left menu, select **Account → Admin roles**.
3. Click **Create new role**.
4. In the **Role info** page, enter a name for the role, such as `cortex-cloud-security-role`.
5. (Optional) Enter a description.
6. Click **Continue**.
7. In the **Select Privileges** page, in the **Privilege Name** list, under **Admin API**, select the following privileges:
   * Organization Units > Read (This automatically selects the Organizational Units > Read permission. Leave it selected.)
   * Users > Read
   * Groups > Read
8. Click **Continue** and then click **Create Role**.

### 2. Assign the Cortex XSIAM service account to the created role

1. In Cortex XSIAM, navigate to **Settings → Data Sources & Integrations** and select **Google Cloud Platform (GCP) → View details**.
2. Identify the GCP cloud instance and click the instance name to open the details pane for that instance.
3. In the details pane, click the **more options** icon at the top right corner and then select **Authorization Details**.
4. Copy the value of Cortex discovery role.
5. Log in to your [Google Admin Console](https://admin.google.com/).
6. In the left menu, select **Account → Admin roles**.
7. Select the role created previously and click **Assign role**.
8. Click **Assign service accounts** and paste the value of the Cortex discovery role. Click **Add**.
9. Click **Assign role**.

Your Cortex XSIAM service account has been successfully granted the necessary permissions in Google Workspace to ingest user, group, and group membership data. It may take several hours for the results to appear in Cortex XSIAM, depending on the size of your cloud estate.

### 3. Enable Google Workspace in your GCP cloud instance

{% hint style="info" %}
Prerequisites

* Ensure you have the organization ID of the Google Workspace you want to connect:
  * Log in to your [Google Admin Console](https://admin.google.com/). and navigate to Account → Account settings → Profile. Next to Customer ID is your organization ID.
* Ensure the organization ID you want to connect meets one of the following requirements:
  * It must already be defined within your Domain Restricted Principles policy.
  * It is the Workspace organization ID to which the GCP organization you have onboarded in this cloud instance belongs.
{% endhint %}

1. In Cortex XSIAM, navigate to **Settings → Data Sources & Integrations** and select **Google Cloud Platform (GCP) → View details**.
2. Identify the GCP cloud instance and click **Configuration** at the right end of the cloud instance row.
3. In the Google Cloud Provider (GCP) onboarding wizard, click **Show advanced settings**.
4. Under **Discovery Enhancements**, select **Connect to GCP Workspace**.
5. Enter the organization ID of your Google Workspace. You can enter more than one organization ID.
6. Click **Save**.

You have successfully enabled the Google Workspace in your GCP cloud instance.
