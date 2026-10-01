---
description: Use MongoDB Atlas data with Cortex XSIAM.
---

# MongoDB Atlas

The capabilities and sub-capabilities listed for this connector are available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud Runtime Security, or Cortex Data Security license.

Secure configurations and monitor identity risks across your MongoDB Atlas environment.

This connector includes the following capabilities and sub-capabilities (if applicable):

* Identity Posture: Maintain visibility and control over MongoDB Atlas identities, including users, groups, roles, and privileges.
* SaaS Posture Configuration Monitoring: Detect, monitor and alert on settings of your SaaS application.
  * saas-posture-config-remediation: Help remediate the misconfigured security settings of your SaaS application.

<details>

<summary><strong>SaaS Posture Configuration Monitoring</strong></summary>

### How to configure the MongoDB Atlas connector <a href="#how-to-configure-the-aha-connector" id="how-to-configure-the-aha-connector"></a>

To access MongoDB Atlas, Cortex XSIAM requires the following information, which you will specify during the connection process.

* **Client ID**: Cortex XSIAM accesses the MongoDB Atlas Administration API through a MongoDB service account that you create. MongoDB Atlas generates a Client ID to uniquely identify the service account.
* **Client Secret**: Cortex XSIAM accesses the MongoDB Atlas Administration API through a MongoDB service account that you create. MongoDB Atlas generates a client secret for the service account. The API verifies the client secret against the client ID to confirm requests are legitimate.

#### **Task 1:** Create a service account in MongoDB Atlas&#x20;

A MongoDB Atlas service account is a non-human, programmatic identity that Cortex XSIAM uses to scan your MongoDB organization. When you create a service account, MongoDB Atlas generates and displays the programmatic credentials (Client ID and Client Secret) that Cortex XSIAM uses to access information about your organization.

{% hint style="info" %}
By following these steps, you onboard only one MongoDB Atlas organization to Cortex XSIAM. If you want Cortex XSIAM to scan multiple organizations, onboard each organization separately.
{% endhint %}

1. Identify the MongoDB Atlas account that you will use to create the service account. \
   Required Permissions: A service account is scoped to one organization. To create a service account, you must be assigned to the Organization Owner role for the organization that you want Cortex XSIAM to scan.
2. Open a web browser to [the MongoDB Atlas website](https://cloud.mongodb.com/) and log in to the Organization Owner account.
3. If you're a member of multiple organizations, make sure you're in the organization that you want Cortex XSIAM to scan. A selection list in the top-left corner of the MongoDB Atlas page shows your current organization. If necessary, select a different organization from this list.
4. From the left navigation pane, select Access Manager.
5. On the Organization Access Manager page, select **Add New > Service Account**.
6. On the Create Service account page, specify the following information:
   * A **Name** for the service account. For example, Cortex XSIAM Service Account.
   * A **Description** of the service account. For example, Service account for Cortex XSIAM authentication.
   * A **Client Secret** Expiration date. The recommended expiration period is 90 days.
   * The **Organization Permissions** to grant to the service account. Select Organization Owner permissions. Cortex XSIAM requires this level of access to complete its scans.
7. Click Create. MongoDB Atlas creates the service account and displays the programmatic credentials (Client ID and Client Secret) that Cortex XSIAM uses for authentication.
8. Copy the Client ID and Client Secret and paste them into a text file. Do not continue to the next step unless you have copied the Client ID and Client Secret. You will provide this information to Cortex XSIAM during the onboarding process.

#### **Task 2:** MongoDB Atlas **to Cortex XSIAM**

1. In Cortex XSIAM, navigate to **Settings** → **Data Sources & Integrations**.
2. Click **+ Add new**.
3. In the **Add Data Sources or Integrations** page, search for MongoDB Atlas.
4. Under **Recommended**, hover over the new MongoDB Atlas integration and click **Add Instance** to launch the configuration wizard.
5. Under the **Capabilities** tab, Enter a Name for your application.
6. Select Security Posture under **Default Capabilities**.
7. Click **Next**.
8. Under **Connection**, enter the Client ID and Client Secret.
9. Under **Configuration** tab, select a **Sync Interval**. Choose a meaningful **Tag** to distinguish between various applications in different environments.
10. A confirmation message indicates that MongoDB Atlas is successfully connected. Confirm the Summary details and click **Save instance**.

</details>

