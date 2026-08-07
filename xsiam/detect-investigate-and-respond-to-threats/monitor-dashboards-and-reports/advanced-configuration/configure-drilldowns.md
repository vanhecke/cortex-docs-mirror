# Configure drilldowns

Enable users to dive deeper into data by configuring dashboard drilldowns on individual widgets. Clicking a configured widget can trigger contextual changes, or seamlessly link users to:

* An XQL search
* A custom URL
* Another dashboard
* A report

Once configured, these drilldowns are instantly available to any authorized user.

{% hint style="info" %}
**Prerequisite:** Some drilldown options require one or more parameters to be configured within the XQL widget query. For more information see [Add parameters to a custom XQL widget](create-custom-widgets/add-parameters-to-a-custom-xql-widget).
{% endhint %}

{% stepper %}
{% step %}
**Open the dashboard builder.**

Select a dashboard from the **Dashboard Manager** and click **Edit**.
{% endstep %}

{% step %}
**Add the drilldown action.**

Identify the widget on which you want to configure a drilldown, click its options menu (the three vertical dots in the widget frame), and select **Add drilldown**.
{% endstep %}

{% step %}
**Configure your drilldown action.**

Choose one of the following configuration options under **Action on Click**:

* **In-Dashboard Drilldown:** Interactively filters the active dashboard using parameters defined in your custom XQL widgets.\
  \&#xNAN;_(Requires parameters to be configured within the XQL widget query)._

<table><thead><tr><th width="145.9998779296875">Field</th><th>Action/Description</th></tr></thead><tbody><tr><td>Parameters</td><td>Select the parameter to filter by. You can choose any parameter defined in the widget's XQL query.</td></tr><tr><td>Value</td><td><p>Define the data point that will trigger the filter when a user clicks the widget. You can:</p><ul><li>Type a static value.</li><li>Select a variable to capture the clicked value dynamically (e.g., $y-axis.value in a chart).</li></ul></td></tr></tbody></table>

{% hint style="info" %}
**Note:** Any other XQL widgets on the dashboard sharing this parameter will also filter automatically.
{% endhint %}

* **Link to Dashboard:** Navigates the user to a separate target dashboard.

{% hint style="info" %}
**Note:** If linking to a **Restricted** dashboard, users must have at least **Viewer** access to view it.
{% endhint %}

<table><thead><tr><th width="177">Field</th><th>Action/Description</th></tr></thead><tbody><tr><td>Dashboard</td><td>Select your target dashboard from the list.</td></tr><tr><td>Parameters (Optional)</td><td>Select parameters to filter the target dashboard. <em>(Available only if the target dashboard's widgets contain defined parameters.)</em></td></tr><tr><td>Value (Optional)</td><td><p>If configuring parameters, select values for filtering the target dashboard. You can:</p><ul><li>Type a static value.</li><li>Select a variable to capture the clicked value dynamically (e.g., <code>$y-axis.value</code>).</li></ul></td></tr></tbody></table>

* **Open XQL Search:** Runs a specific XQL query based on the clicked value.

<table><thead><tr><th width="184">Field</th><th>Action/Description</th></tr></thead><tbody><tr><td>XQL Query</td><td><p>Enter the query you want to execute upon drilldown.</p><p>Type $ to open the autocomplete menu for available widget variables (e.g., in a table widget, <code>$first.name</code> selects the leftmost column).</p></td></tr></tbody></table>

{% hint style="info" %}
**Example XQL:** This example passes two parameters from a table widget into an XQL query: the specific cell value clicked, and the cell value from the `request_url` column in that same row.

```
dataset=xdr_data

|filter event_type=$y_axis.value and requestUri=$row.request_url

|fields action_download, action_remote_ip as remote_ip,

actor_process_image_name as process_name

|comp count_distinct(action_download) as total_download by process_name,

remote_ip, remote_hostname

|sort desc total_download

|limit 10

|view graph type=single subtype=standard xaxis=remote_ip yaxis=total_download
```
{% endhint %}

* **Open Custom URL:** Opens an external web page based on the clicked value.

<table><thead><tr><th width="148.9998779296875">Field</th><th>Action/Description</th></tr></thead><tbody><tr><td>URL Address</td><td>Enter the destination URL. To make the link dynamic, insert variables from the Available parameters list.</td></tr></tbody></table>

{% hint style="info" %}
**Example URL:** In this URL, the `$x_axis.value` variable represents Cortex product names. Clicking a slice in a pie chart replaces the variable with the specific product name:

`https://www.paloaltonetworks.com/cortex/cortex-$x_axis.value`
{% endhint %}

* **Generate Report:** Instantly runs a report using data from the clicked value.
{% endstep %}

{% step %}
**Save the widget.**

Click **Save** on the widget dialog, and ensure you save your overall changes to the dashboard before exiting the editor.
{% endstep %}
{% endstepper %}

### **Variables in drilldowns**

The following tabs are organized according to widget type and describes the widget variables that are available in drilldowns. The variable defines the value to capture in the drilldown, according to the element that is clicked. The captured value is then configured as a parameter by which to filter data on drilldown.

{% tabs %}
{% tab title="Chart" %}
(Area, Bubble, Column, Funnel, Line, Map, Pie, Scatter, or Word Cloud)

![DD\_example\_chart.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-44c9c3afaf2e65d6c41a892e0497ebec4b33d0a8%2Fbe3be091e84a429641531f0857a4ff13c50f6af17fcb27a87ad41fbdc8cac70a.png?alt=media)

* **`$x_axis.name`**: Selects the x-axis name.
* **`$x_axis.value`**: Selects the x-axis value for the clicked value.
* **`$y_axis.name`**: Selects the y-axis name.
* **`$y_axis.value`**: Selects the y-axis value for the clicked value.
{% endtab %}

{% tab title="Single value or gauge" %}
![DD\_example\_gauge.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-063c3ad27d2f429e940e5b614d2290fcc7dcd22c%2F88118a7265d707ed4a7c7b1bdbaf72e37c19527415c121b96ead037ab26569ae.png?alt=media)

* **`$y_axis.name`**: Selects the y-axis name that the single value represents.
* **`$y_axis.value`**: Selects the y-axis value for the clicked value.
{% endtab %}

{% tab title="Table" %}
![DD\_example\_table.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b3978c396b4d329748c8e0e4f309277eb3bbf010%2F481b2b5e1ecf964ed4dae16057c42cc9593cb341076370b5fe6e8cec885d6776.png?alt=media)

* **`$first.name`**: Selects the leftmost column name in the table.
* **`$first.value`**: Selects the leftmost value in the clicked table row.
* **`$clicked.name`**: Selects the column name of the clicked value.
* **`$clicked.value`**: Selects the value in the clicked table cell.
* **`$row.<field_name>`**: Selects the field (column) from the clicked table row.
{% endtab %}
{% endtabs %}

c
