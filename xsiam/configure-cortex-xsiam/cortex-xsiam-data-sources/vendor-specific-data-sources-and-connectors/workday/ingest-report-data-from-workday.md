# Ingest report data from Workday

To receive Workday report data, you must first configure data collection from Workday using a Workday custom report to ingest the appropriate data. This is configured by setting up a Workday Collector in Cortex XSIAM and configuring report data collection via this Workday custom report that you set up.

As soon as Cortex XSIAM begins receiving data, the app automatically creates a Workday Cortex Query Language (XQL) dataset (`workday_workday_raw`). You can then use XQL Search queries to view the data and create new Correlation Rules. In addition, Cortex XSIAM adds the Workday fields next to each user in the Key Assets list on the Cases page, and in the User node in the Causality View of Identity Analytics issues.

{% hint style="info" %}
**Note**

Any user with permissions to view issues and cases can view the Workday data.
{% endhint %}

You can only configure a single Workday Collector, which is automatically configured to run the report every 6 hours. You can always use the Sync Now option to run the report whenever you want.

{% hint style="info" %}
**Prerequisite**

1. Create an Integration System User that is designated to access the custom report from Workday for data collection in Cortex XSIAM.
2. Create an Integration System Security Group for the Integration System User created in Step 1 for accessing the report. When setting this group ensure to define the following:
   * Type of Tenanted Security Group: Select either Integration System Security Group (Constrained) or Integration System Security Group (Unconstrained) depending on how your data is configured. For more information, see the Workday documentation.
   * Integration System User: Select the user that you defined in step 1 for accessing the custom report.
3. Create the Workday credentials for the Integration System User created in Step 1 so that the username and password can be used to access the report in Cortex XSIAM. Record these credentials as you will need them when configuring the Workday Collector in Cortex XSIAM.
{% endhint %}

{% hint style="info" %}
**Note**

For more information on completing any of the prerequisite steps, see the Workday documentation.
{% endhint %}

Configure Cortex XSIAM to receive report data from Workday:

1. Configure a Workday custom report to use for data collection.
   1. Log in to the [Workday Resource Center](https://signin.resourcecenter.workday.com/).
   2. In the search field, specify Create Custom Report to open the wizard.
   3. Configure the following Create Custom Report settings:
      * **Report Name:** Specify the name of the report.
      * **Report Details section:**
        * **Report Type:** Select Advanced. When you select this option, the Enable As Web Service checkbox is displayed.
        * **Enable As Web Service:** Select this checkbox, so that you will be able to generate a URL of the report to configure in Cortex XSIAM.
      * **Data Source section:**
        * **Optimized for Performance:** Select whether the data should be optimized for performance. The way this checkbox is configured determines the Data Source options available to choose from.
        * **Date Source:** Select the applicable data source containing the data that is used to configure data collection from Workday to Cortex XSIAM.
   4.  Click OK, and configure the following Additional Info settings. The Additional Info table in the Columns tab is where you can perform the following.

       * For the incident and card views in Cortex XSIAM, map the required fields from the Data Source configured by selecting the applicable Field that you want to map to the Cortex XSIAM field name required for data collection in the Column Heading Override XML Alias column.
       * (Optional) You can map any additional fields from the Data Source configured that you want to be able to query in XQL Search using the `workday_workday_raw` dataset. This is configured by selecting the applicable Field and leaving the default field name that is displayed in the Column Heading Override XML Alias column. This default field name is what is used in XQL Search and the dataset to view and query the data.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The Business Object changes depending on the Data Source selected.</p></div>

       For the incident and card views in Cortex XSIAM, map the following fields in the table by selecting the applicable Field that contains the data representing the Cortex XSIAM field name as provided below that should be added to the Column Heading Override XML Alias. For example, for `full_name`, select the applicable Field from the Business Object defined that contains the full name of the user and in the Column Heading Override XML Alias specify `full_name` to map the set Field to the Cortex XSIAM field name.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Cortex XSIAM uses a structured schema when integrating Workday data. To get the best Analytics results, specify all the fields marked with an asterisk from the recommended schema.</p><ul><li><code>workday_user_id*</code></li><li><code>full_name*</code></li><li><code>workday_manager_user_id*</code></li><li><code>manager*</code></li><li><code>worker_type*</code></li><li><code>position_title*</code></li><li><code>department*</code></li><li><code>private_email_address*</code></li><li><code>business_email_address*</code></li><li><code>employment_start_date*</code></li><li><code>employment_end_date</code></li><li><code>phone_number</code></li><li><code>mailing_address</code></li></ul></div>

       e. (Optional) Filter out any employees that you do not want included in the Filter tab.

       f. Share access to the report with the designated Integration System User that you created by setting the following settings in the Share tab:

       * **Report Definition Sharing Options:** Select Share with specific authorized groups and users.
       * **Authorized Users:** Select the designated Integration System User that you created for accessing the custom report.

       g. Ensure that the following Web Services Options settings in the Advanced tab are configured. Here is an example of the configured settings, where the Web Service API Version and Namespace are automatically populated and dependent on your report.\
       ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2F2fkvVbmuSZM3efJXquYv%2Fimage.png?alt=media\&token=53683da4-78f2-4a58-a5d3-f3898174e2c9)

       h. (Optional) Test the report to ensure all the fields are populated.\
       \
       i. Get the URL for the report.

       1. In the related actions menu, select **Actions → Web Service → View URLs**.
       2. Click **OK**.
       3. Scroll down to the **JSON** section.
       4. Hover over the **JSON** link and click the icon, which open a new tab in your browser with the URL for the report. You need to use the designated user credentials to open the report.
       5. Copy the URL for the report and record them somewhere as this URL needs to be provided when setting up the Workday Collector in Cortex XSIAM.

       j. Complete the report by clicking **Done**.
2.  Configure the Workday collection in Cortex XSIAM.

    a. Navigate to **Settings → Data Sources & Integrations**.

    b. On the **Data Sources & Integrations** page, click **+ Add New**, search for **Workday**, then hover over it and click **Add**.

    c. Set the following parameters.

    * **Name:** Specify the name for the Workday Collector that is displayed in Cortex XSIAM.
    * **URL:** Specify the URL of the custom report you configured in Workday.
    * **User Name:** Specify the username for the designated Integration System User that you created for accessing the custom report in Workday.
    * **Password:** Specify the password for the designated Integration System User that you created for accessing the custom report in Workday.

    d. Click **Test** to validate access, and then click **Enable**.

    A notification appears confirming that the Workday Collector was saved successfully, and closes on its own after a few seconds.

    Once report data starts to come in, a green check mark appears underneath the **Workday Collector** configuration with the data and time that the data was last synced.
3.  (Optional) Manage your Workday Collector.

    After you enable the Workday Collector, you can make additional changes as needed. To modify a configuration, select any of the following options.

    * **Edit** the Workday Collector settings.
    * **Disable** the Workday Collector.
    * **Delete** the Workday Collector.
    * **Sync Now** to run the report to get the latest report data. The report is run automatically every 6 hours, but you can always get the latest data as needed.
4. After Cortex XSIAM begins receiving report data from Workday, you can use the XQL Search to search for logs in the new dataset (`workday_workday_raw`).
