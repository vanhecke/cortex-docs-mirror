---
description: Add Snowflake as a Cortex XSIAM data source.
---

# How to onboard Snowflake

## How to onboard Snowflake

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

Integrate Cloud Data Security with your Snowflake account to gain comprehensive visibility into any data and posture risk existing in your Snowflake environment. This integration enables automated scanning of all assets in Snowflake, including data classification and risk assessment.

You can add Snowflake as a third-party data source in Cloud Data Security.

{% hint style="warning" %}
### Prerequisite

* To use Snowflake, you must be registered with one of these cloud providers: Amazon AWS, Microsoft Azure, or Google Cloud Platform (GCP).
* Ensure you have the necessary account permissions to onboard. It is recommended to use Account Admin as the role for the onboarding.
{% endhint %}

**Configuration Step**

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**.
3. On the **Add Data Sources or Integrations** page, search for **Snowflake**, then hover over it and click **Add**.
4. On the **New Data Source** Snowflake integration instance settings page, do the following:
   1. Enter a display name for your Snowflake integration instance.
   2.  Enter a Data Sharing Account Identifier.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The account identifier can be found using the user information at the bottom left. Hover over the account you wish to onboard and select the copy option at the top right. The account identifier is usually of the format:</p><p>(organization).[account]</p></div>
   3. (Optional) If you have a Snowflake account that is protected by a network policy, turn on the **My Snowflake account is protected by network policies** toggle button. The network policies are related to the IP allow list.
   4. Select a cloud platform and choose a region.
   5. (Optional) If you want to use an existing user:
      1. Click **Show advance settings** and then turn on the **Use an existing user** toggle button.
      2. Enter the user name and the login name.
5. Click **Next**.

**Establish Connection Step**

1. Open your Snowflake console in a new tab.
2. Using the copy or download icons, copy or download the script in the **Generated script** text box and paste it into a new worksheet in Snowflake.
3. Select the entire script and select **Run all**.
4. Once the script runs without errors, come back to the **Snowflake** screen and click **Verify Connection** to check if the instance is detected.

**Verify Connection Step**

1. A success or failure message appears on the screen.
2. If a success message appears, you can do the following:
   * View the instance's information in the Snowflake Posture instances.
   * View the assets in Asset Inventory, once the first scan is complete.

**Delete a Snowflake instance**

1. Navigate to **Settings** → **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, select the **Snowflake** integration or filter to search for it and then select it.
3. On the **Snowflake** page, right click the row of the integration instance you want to delete.
4.  From the drop down menu, select **Settings** and from the integration instance settings page select the **Delete** checkbox and then click **Delete**.

    The Snowflake instance is now removed, including all previous scans.
