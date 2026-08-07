---
description: Add Databricks as a Cortex Cloud Data Security data source.
---

# How to onboard Databricks

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

**Overview**

You can add the Databricks platform as a third-party data source in Cortex Cloud Data Security.

**Prerequisites**

* To use Databricks, you must be registered.
* Make sure you have the following account permissions to onboard:
  * `Account Admin`: For information about this role, see [Set up users, groups, and roles](../../../onboard-cortex-xsiam/deployment-steps/set-up-users-and-roles).
  * `Metastore Admin`: Databricks admin that can only be assigned by an `Account Admin`. Databricks recommends assigning this role to a group rather than an individual user to facilitate management and ensure continuity in case an individual leaves the organization.
* Make sure you have the following ID numbers at hand:
  *   **Account ID:** Refers to the unique identifier of the user account.

      How to find the Account ID

      1. Log in to the account console.
      2. In the account console, your username should appear in the upper right corner of the page.
      3. Click the icon of your username.
      4. Your account ID appears in the list.
  *   **Application ID:** Refers to the unique identifier for a service principal in Databricks.

      How to find the Application ID

      1. Log in to the account console.
      2. Click **User Management** and navigate to the **Service Principals** tab.
      3. Click the name of the service principal for which you need the Application ID. The service principal must also be the account admin.
      4. On the service principal settings page, navigate to the **Configuration** tab.
      5. The Application ID appears in the list.

### **Add the Databricks data source**

To add the Databricks platform as a data source, you need to add configuration details, establish a connection, and then verify the connection.

Add configuration details

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**.
3. On the **Add Data Sources or Integrations** page, search for **Databricks**, then hover over it and click **Add**.
4. On the **Databricks** integration instance settings page, for the **Configuration** step, do the following:
   1. Enter the display name for your Databricks integration instance.
   2. Enter your Databricks Account ID.
   3. Enter your Application ID.
   4. Select a cloud platform.
   5.  (Optional) Turn on the toggle for **My Databricks account protected by network policies** and select a region.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you turn on this feature, both the cloud and region will be used for scanning, possibly incurring cost and requiring adherence to certain compliance policies.</p></div>
   6. Click **Next**.
5. Click **Next**.

### Establish a connection

1. For the **Establish Connection** step, you are now instructed to open your Databricks console in a new browser tab.
2. On the **Establish Connection** tab, click the arrow to open the **Generated script** code block. Do one or both of the following:
   * Click the cloud icon to download the .sh script file.
   * Click the copy icon to copy the script to your clipboard.
3. Run the script in your Databricks CLI.
4. Click **Verify Connection**.

Verify the connection

1. For the **Verify Connection** step, if the connection is verified, a confirmation message is displayed.
2. Click **Close**.

**Databricks** now appears in the list of data sources on the **Data Sources & Integrations** page.

### **Verify the Cortex Gateway connection**

At the end of the onboarding process, a pending request for Databricks approval is automatically created and displayed on the Cortex Gateway screen. To complete the onboarding process, approve the pending request. If you do not have permissions, contact your Cortex Cloud administrator.

For more information, see [Egress configurations](https://app.gitbook.com/s/SqEFcjERpi4JSgB9LjVw/egress-configurations).
