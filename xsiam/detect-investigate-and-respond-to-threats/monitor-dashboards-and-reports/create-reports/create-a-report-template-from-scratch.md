---
description: >-
  Create a Cortex XSIAM report template from scratch for repeatable security
  reporting.
---

# Create a report template from scratch

You can use report templates to standardize and automate your data delivery—allowing you to generate one-time or recurring reports on a schedule and seamlessly distribute them to different user groups or mailing lists.

Use the following high-level workflow to create and distribute a report, guiding you from initial setup through layout design and distribution.

{% stepper %}
{% step %}
### Open the report builder

Depending on your starting point, open the report builder as follows:

* **Build a report from scratch:** Go to **Dashboards & reports > Reports** and click **Create template**.
* **Use a system template:** Go to **Dashboards & reports > Reports** and click **Create template**. In the report builder, click **Browse templates** to see the available options.
* **Save a dashboard as a report template:** You can save a dashboard as a report template during dashboard creation, or from the **Dashboard Manager** choose a dashboard and select **Save as report template**.

Click **Edit** to make changes to the template or to run the report without making changes, select **Generate report**.
{% endstep %}

{% step %}
### Build your report layout

1. **Add or remove widgets from your canvas:** Drag widgets directly onto the canvas from the **Widget Library**:
   * **Predefined Widgets:** Search the **Widget library** (filter by Owner, Category, Chart type, or data source) and drag your selected widgets onto the canvas. Click on a widget to see a graphical preview and configuration details.
     * **Tip:** To find widgets that can be modified, select the **Editable widget only** option. These widgets can be duplicated and edited to suit your specific needs without starting from scratch.
   * **Custom Widgets:** If the library does not contain the widgets you require, you can create custom widgets using XQL queries, scripts, or generate them using AI. For more information, see [Create custom widgets](../advanced-configuration/create-custom-widgets).
2. _(Optional)_ **Refine widget data:** For certain widgets you can refine the displayed data as follows:
   * For agent-related widgets, you can apply an endpoint scope to refine the displayed data to only show results from specific endpoint groups. Select the menu on the top right corner of the widget, select **Groups**, and select one or more endpoint groups.
   * For case-related widgets, you can refine the displayed data to only show results from cases that match a case starring configuration. A purple star indicates that the widget is displaying only starred cases. For more information, see \<Case starring>.
{% endstep %}

{% step %}
### Configure filters

If your report contains custom XQL widgets with defined parameters, you can add configure filters to refine the data in your report. Follow the steps in [Configure Global Filters](../advanced-configuration/configure-global-filters).
{% endstep %}

{% step %}
### Finalize the layout

1. **Name your report:** Enter a unique, descriptive name in the title field.
2. _(Optional)_ **Add static text:** Click **Static Elements** to add headers, titles, or free text blocks.
3. **Arrange the layout:** Reports are formatted in A4 pages. You can scroll all pages in the report in the navigation panel. To optimize the space in the report, select **Auto arrange layout** from the **Settings** menu, or arrange the widgets manually.
{% endstep %}

{% step %}
### Save and define report settings

1. **Open save settings:** Click the **Save** button in the report builder header.
2. **Add a description:** Provide a detailed description explaining the purpose of the report to help other users identify its use case.
3. **Configure timeframe:** Select the timeframe for the widget data.
4.  **Configure automated distribution and scheduling settings:** including email recipients, Slack notifications, delivery, and scheduling.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To send reports to Slack, Slack must be configured as an external application. For more information, see <a href="../../../onboard-cortex-xsiam/post-deployment/data-and-log-forwarding/forward-logs-and-data-from-cortex-xsiam-to-external-services/configure-external-applications-for-forwarding/integrate-slack-for-outbound-notifications">Integrate Slack for outbound notifications</a>.</p></div>
5. **Configure CSV data attachments:** Select Attach CSV to include raw data from XQL widgets. From the menu, select one or more of your custom widgets to attach to the report. The CSV files of the widgets are attached to the report along with the report PDF. Depending on how you selected to send the report, the CSV file is attached as follows:
   * **Email:** Sent as separate attachments for each widget. The total size of the attachment in the email cannot exceed 20 MB.
   * **Slack:** Sent within a ZIP file that includes the PDF file.
6.  **Save the report:** Click **Save** to commit all changes.

    **Tip:** You can configure a notification rule to send an email or send a notification to a syslog server if a report fails to run due to a timeout or fails to upload to the GCP bucket. For more information see [Configure the notification rule for a failed report](../manage-dashboards-and-reports/configure-the-notification-rule-for-a-failed-report).
{% endstep %}

{% step %}
### Share the report template

By default, all new custom report templates are **Restricted** and visible only to you (the Owner). Once created, you can share the report template with specific users or groups, or make it **Public** to all authorized users.

{% hint style="info" %}
Sharing of report templates must be enabled by your administrator. For more information, see [Manage access to objects](../../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-access-to-objects).
{% endhint %}

**How to share a dashboard**

1. **Open share settings:** In the **Report templates** tab, find the template name and select **Share** from the right-click menu.
2. **Update your visibility settings:**
   * **To share globally:** Under **General access**, change the setting to **Public** so all authorized users in your organization can view it.
   * **To share selectively:** Keep the status as **Restricted**, add specific users or groups, and assign them a role (**Viewer** or **Editor**).
3. **Save your changes:** Click **Share** to apply your settings.
{% endstep %}
{% endstepper %}
