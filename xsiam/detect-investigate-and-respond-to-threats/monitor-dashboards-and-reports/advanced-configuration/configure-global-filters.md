# Configure global filters

Define global filters on your dashboards to enable users to alter the scope of the data by selecting from predefined or dynamic values. You can define filters using free text, single-select, or multi-select input values. Once configured, these filters are accessible to anyone viewing the dashboard.

You can configure up to four global filters on a single dashboard or report.

{% hint style="info" %}
**Prerequisite:** Before configuring global filters, you must add parameters to one or more custom XQL widgets on your dashboard. For more information, see [Add parameters to a custom XQL widget](create-custom-widgets/add-parameters-to-a-custom-xql-widget).
{% endhint %}

{% stepper %}
{% step %}
**Open the dashboard builder.**

Select a dashboard from the **Dashboard Manager** and click **Edit**.
{% endstep %}

{% step %}
**Open the filter configuration.**

In the Widget Library click the **Filters & Inputs** icon.
{% endstep %}

{% step %}
**Define the Input name.**

Enter a name that identifies the parameter for dashboard users.
{% endstep %}

{% step %}
**Select the filter type.**

Choose one of the following options:

* **Single Select:** To specify a single predefined value.
*   **Multi Select:** To specify multiple predefined or dynamic values.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Multi-select and dynamic filters require the IN operator to be configured within the XQL widget query.</p></div>
* **Free text/number:** To specify a single free-text value.
{% endstep %}

{% step %}
**Select the parameter.**

From the dropdown, choose the specific parameter from your XQL widgets that you want to configure.
{% endstep %}

{% step %}
**Define dropdown options.**

For **Single Select** or **Multi Select** filters, specify filter values. When the dashboard is generated, these options will appear in a dropdown list.

*   **For Predefined inputs:** Manually type the list values.

    Guidelines for predefined inputs

    * The values must support the parameter type. For example, specify characters for $name and numbers for $num.
    * If you uploaded numbers in a string, enclose each number in quotes (e.g., `"500"`).
*   **For Dynamic inputs:** Configure a query to fetch dynamic values. Click **Select** under **Define Query**.

    #### **Guidelines for dynamic inputs**

    * The query must include the fields stage to select the specific column name for the dropdown values. All values in this field will be available for selection and will update dynamically.
    * <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Example:</strong><br>In this example, the <strong>endpoint_name</strong> field is configured so users can filter by one or more endpoint names:<br><code>dataset = endpoints | fields endpoint_name</code></p></div>
    * <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> If you specify more than one field, only the first field's values will be used.</p></div>
{% endstep %}

{% step %}
**(Optional) Define a default value.**

If you define a default, the widget populates automatically when the dashboard opens. If no default value is defined, the user can select a value when they open the dashboard.
{% endstep %}
{% endstepper %}
