# Graph query results

To help you better understand your Cortex Query Language (XQL) query results and share your insights with others, Cortex XSIAM enables you to generate graphs and outputs of your query data directly from query results page.

{% hint style="info" %}
### Tip

Alternatively, you can use the Cortex Agentic Assistant to generate custom graphs and charts using natural language prompts. By simply prompting the agent, it will build and execute the query, returning the visual representation. For more information, see [Use natural language to query and visualize your data](../../../agentic-assistant-chat/use-natural-language-to-query-and-visualize-your-data).
{% endhint %}

1. Select **Investigation & Response** → **Search** → **XQL Search**.
2.  Run an XQL query.

    Enter the following query:

    ```programlisting
    dataset = xdr_data 
    | fields action_total_upload, _time 
    | limit 10
    ```

    The query returns the `action_total_upload`, a number field, and `_time`, a string field, for up to 10 results.
3. In the **Query Results** section, to graph the results either:

<details>

<summary>Use Chart Editor</summary>

Navigate to **Query Results** → **Chart Editor ()** to manually build and view the graph using the selected graph parameters:

* **Main**
  *   **Graph Type**: Type of graphs and output options available: **Area**, **Bubble**, **Column**, **Funnel**, **Gauge**, **Line**, **Map**, **Pie**, **Scatter**, **Single Value**, or **Word Cloud**.

      <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><p>To display the result of as a time duration, choose the graph type <strong>Single Value</strong> and enable <strong>Show as Time</strong>. You can then select the <strong>Time Unit</strong> (millisecond, second, minute, or hour) and the <strong>Display format</strong>.</p></div>
  * **Subtype** and **Layout**: Depending on the selected type of graph, choose from the available display options.
  * **Header**: Title your graph.
  * **Show Callouts**: Display numeric values on the graph.
* **Data**
  * **X-axis**: Select a field with a string value.
  * **Y-axis**: Select a field with a numeric value.
  * (Optional) **Series**: For an area, bubble, column, line, map, or scatter chart, you can specify a field (column) to group chart results based on y-axis values. This option is only displayed when one of the supported graph types are selected, and a single y-axis value is selected.
* Depending on the selected type of graph, customize the **Color**, **Font**, and **Legend**.

</details>

<details>

<summary>Use XQL query</summary>

Enter the visualization parameters in the XQL query section.

You can express any chart preferences in XQL. This is helpful when you want to save your chart preferences in a query and generate a chart every time that you run it. To define the parameters, either:

*   Define the following query:\
    Example<br>

    ```
    dataset = xdr_data 
    | view graph type = column header = "Test 1" xaxis = _time yaxis = action_total_upload series = _vendor
    ```
* Select ADD TO QUERY to insert your chart preferences into the query itself.

</details>

4.  (Optional) Create a custom widget.

    To easily track your query results, you can create custom widgets based on the query results. The custom widgets you create can be used in your custom dashboards and reports. For more information, see Create custom XQL widgets.<br>

    Select **Save to Widget Library** to pivot to the Widget Library and generate a custom widget based on the query results.
