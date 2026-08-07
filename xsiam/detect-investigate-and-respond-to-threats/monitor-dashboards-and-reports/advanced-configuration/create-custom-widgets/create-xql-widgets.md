# Create XQL widgets

Custom XQL widgets allow you to build charts based on specific Cortex Query Language (XQL) queries. To create an XQL widget, from the **Widget Library** click **Create widget > XQL widget**.

{% stepper %}
{% step %}
### Basic configuration

1. Enter a widget name and description.
2. Select the visibility level (**Public** or **Restricted**).
   * **Restricted (Default):** Leave unselected to keep the widget visible only to you.
   * **Public:** Select this to make the widget visible to all users with **Widget Library** access.

{% hint style="info" %}
**Note:** For more information on how widget access works, see [Access to widgets](../../access-and-visibility-for-dashboards-and-reports/access-to-widgets).
{% endhint %}
{% endstep %}

{% step %}
### Define your query

1.  In the query editor, define your XQL query.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Tip:</strong> Select <strong>XQL Helper</strong> to view commonly used commands with example syntax. For more information, see <a href="../../../investigation-and-response/build-xql-queries/how-to-build-xql-queries">How to build XQL queries</a>.</p></div>
2. (Optional) Add parameters to your query to configure filters and drilldowns on your dashboard. For more information see [Add parameters to a custom XQL widget](add-parameters-to-a-custom-xql-widget).
3.  (Optional) Change the default time period using the time picker at the top right of the window. Select from the following options:

    * **Standard time frames:** Predefined ranges, such as _Last 24 hours_ or _Last 30 days_.
    * **Relative time**: Define a custom window (e.g., the last `<number>` of minutes, hours, or days).
    * **Calendar:** Create a customized, static date/time period.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Changing the query window's time period automatically updates the config timeframe, however it is not visible in the query unless you add it manually.</p></div>
4. Click **Preview** to validate your data results.

{% hint style="info" %}
**Note:** XQL queries generated within the Widget Library do not appear in the Query Center; their results are used exclusively to build the custom widget.
{% endhint %}
{% endstep %}

{% step %}
### Define the graph visualization

In the **Widget** tab, select **Graph** and use the **Chart Editor** to configure the following fields:

* **Graph type & Subtype:** Select your visualization style (e.g., Area, Column, Pie, Single Value, Table).
* **Headers & labels:** Define header text and choose whether to display callouts or percentages.
* **Axis Mapping:** Map your data fields to the X-axis (string values) and Y-axis (numeric values).
* **Series (Optional):** Specify a field (column) to group chart results based on Y-axis values. **Note:** This option only appears for supported graph types when a single Y-axis value is selected.
* **Group additional values (Optional):** Select **Group additional values as Others** and set the maximum number of values to display. This reduces clutter by limiting the number of data values to display and grouping additional values in an “Others” category.
* **Apply default limit (Optional):** Select this to limit the number of returned results for optimal loading times. Alternatively, you can add the limit stage directly to your query.
* **Baseline (Optional):** Add a baseline reference value to the graph (available for select graph types).
* **Styling (Optional):** Customize colors, fonts, and legend placements as required.
{% endstep %}

{% step %}
### Finalize and save widget

1. (Optional) Click **Add to query** to insert your chart preferences directly into the query syntax.
2. Click **Save widget** to add the widget to your library.
{% endstep %}
{% endstepper %}
