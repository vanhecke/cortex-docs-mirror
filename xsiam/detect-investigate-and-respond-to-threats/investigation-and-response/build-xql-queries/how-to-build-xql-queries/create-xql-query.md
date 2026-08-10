# Create XQL query

Review the following topics:

* [How to build XQL queries]()

Build Cortex Query Language (XQL) queries to analyze raw log data stored in Cortex XSIAM. You can query the Cortex Data Model (XDM) or datasets using specific syntax.

<details>

<summary>How to create a XDM query</summary>

1. From Cortex AgentiX, select **Investigation & Response** → **Search** → **Query Builder**.
2. Click **XQL**.
3.  _(Optional)_ Change the default time period against which to run your query from the time picker at the top right of the window. You can select the required time period from any of the following options available:

    * Preset time ranges easily available to select from, such as **24 hours** and **30 days**.
    * Recently used selections from your previous queries.
    * **Relative time**: Define the time frame as the last \<number> minutes, days, or hours by setting the number.
    * **Calendar**: Create a customized time period by selecting the date range from the calendar and the specific **Start Time** and **End Time**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>Whenever the time period is changed in the query window, the <code>config timeframe</code> is automatically set to the time period defined for the entire query, including queries that are part of the <code>join</code> stage. Yet, this won't be visible as part of the query. Only if you manually type in the <code>config timeframe</code> will this be seen in the query.</li><li>These time picker options are available in XQL queries when using the Query Builder, XQL Widgets, and when defining XQL Widgets in Reports and Dashboards.</li></ul></div>
4. _(Optional)_ To translate Splunk queries to XQL queries, enable **Translate to XQL**. If you choose to use this feature, enter your Splunk query in the **Splunk** field, click the arrow icon to convert to XQL, and skip to Step 6.
5.  Create your query by typing in the query field. Relevant commands, their definitions, and operators are suggested as you type.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>When creating XQL queries, you can:</p><ul><li>Use the up and down arrow keys to navigate through the auto-suggestion command suggestions and definitions.</li><li>Select an auto-suggestion command by pressing either the <strong>Enter</strong> or <strong>Tab</strong> key.</li><li>Press <strong>Shift</strong>+<strong>Enter</strong> to add a new line, and easily ignore the auto-suggestion output.</li><li>Close the auto-suggestion output by pressing the <strong>Esc</strong> key.</li></ul></div>

    1.  Specify the datasets to run your query against by typing either `datamodel dataset = <dataset name>...` or `datamodel dataset in (<dataset name>,...)...`. For example:

        ```programlisting
        datamodel dataset in (amazon_aws_raw)
        ```

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>While <code>datamodel dataset=*</code> is supported in the query, we recommend that you specify specific datasets for quicker and more efficient results.</p></div>
    2. Press Enter, and then type the pipe character (**`|`**). Select a stage, and complete the stage syntax using the suggested options.
    3.  Continue adding stages until your query is complete. For example:

        ```programlisting
        datamodel dataset in (amazon_aws_raw)
            | filter xdm.source.ipv4 = "10.9.165.1"
            | fields xdm.source.ipv4, xdm.source.port
            | limit 100  
        ```
6. Choose when to run your query:
   * Run the query immediately.
   * Run the query by the specified date and time, or on a specific date, by selecting the calendar icon (![query-calendar-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ecc2f1d84a0c8f48991afeadea0050026af46e29%2Feb3b32c669ba53c9a0fdf3d660dfdbd58a8a443bfb8f847de1b32e6b2948cdcc.png?alt=media)).
7. _(Optional)_ The Save As options save your query for future use:

* **Correlation Rule**: When compatible, saves the query as a Correlation Rule. For more information, see [What's a correlation rule?](../../../threat-management/detection-rules/what-are-detection-rules/whats-a-correlation-rule).
  * **Query to Library**: Saves the query to your personal query library. For more information, see [Manage your personal query library](../manage-your-personal-query-library).
* **Widget to Library**: For more information, see [Create XQL widgets](../../../monitor-dashboards-and-reports/advanced-configuration/create-custom-widgets/create-xql-widgets).

{% hint style="info" %}
### Tip

While the query is running, you can navigate away from the page. A notification is sent when the query has finished. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
{% endhint %}

</details>

<details>

<summary>How to create a dataset query</summary>

1. From Cortex XSIAM, select **Investigation & Response** → **Search** → **XQL Search**.
2.  _(Optional)_ Change the default time period against which to run your query from the time picker at the top right of the window. You can select the required **Timeframe** from any of the following options available:

    * Preset time ranges easily available to select from, such as **24 hours** and **30 days**.
    * Recently used selections from your previous queries.
    * **Relative time**: Define the time frame as the last \<number> minutes, days, or hours by setting the number.
    * **Calendar**: Create a customized time period by selecting the date range from the calendar and the specific **Start Time** and **End Time**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>Whenever the time period is changed in the query window, the <code>config timeframe</code> is automatically set to the time period defined for the entire query, including queries that are part of the <code>join</code> stage. Yet, this won't be visible as part of the query. Only if you manually type in the <code>config timeframe</code> will this be seen in the query.</li><li>These time picker options are available in XQL queries when using the Query Builder, XQL Widgets, and when defining XQL Widgets in Reports and Dashboards.</li></ul></div>
3. _(Optional)_ To translate Splunk queries to XQL queries, enable **Translate to XQL**. If you choose to use this feature, enter your Splunk query in the **Splunk** field, click the arrow icon (<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-71323bbde54be11af6b419e0c345f2d01f50d2f5%2F49c8fc73157209b7a766a070aef61257efb9b7d6ddc22957f2c8ae2c8e9084a2.png?alt=media" alt="translate-to-spl-arrow.png" data-size="line">) to convert to XQL, and skip to Step 6.
4.  Create your query by typing in the query field. Relevant commands, their definitions, and operators are suggested as you type.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>When creating XQL queries, you can:</p><ul><li>Use the up and down arrow keys to navigate through the auto-suggestion command suggestions and definitions.</li><li>Select an auto-suggestion command by pressing either the <strong>Enter</strong> or <strong>Tab</strong> key.</li><li>Press <strong>Shift</strong>+<strong>Enter</strong> to add a new line, and easily ignore the auto-suggestion output.</li><li>Close the auto-suggestion output by pressing the <strong>Esc</strong> key.</li></ul></div>

    1.  (Optional) Specify a dataset.

        You only need to specify a dataset if you are running your query against a dataset that you have not set as default. Otherwise, the query runs against the **`xdr_data`** dataset. For more information, see [How to build XQL queries]().

        Example:

        ```programlisting
        dataset = xdr_data
        ```
    2. Press **Enter**, and then type the pipe character (**`|`**). Select a command, and complete the command using the suggested options.
    3.  Continue adding stages until your query is complete.



        ```programlisting
        dataset = xdr_data 
        | filter agent_os_type = ENUM.AGENT_OS_MAC
        | limit 250  
        ```
5. Choose when to run your query:
   * Run the query immediately.
   * Run the query by the specified date and time, or on a specific date, by selecting the calendar icon (![query-calendar-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ecc2f1d84a0c8f48991afeadea0050026af46e29%2Feb3b32c669ba53c9a0fdf3d660dfdbd58a8a443bfb8f847de1b32e6b2948cdcc.png?alt=media)).
6. _(Optional)_ The Save As options save your query for future use:
   * **BIOC Rule**: When compatible, saves the query as a BIOC rule. The XQL query must contain a filter for the **event\_type** field.

* **Correlation Rule**: When compatible, saves the query as a Correlation Rule. For more information, see [What's a correlation rule?](../../../threat-management/detection-rules/what-are-detection-rules/whats-a-correlation-rule).
  * **Query to Library**: Saves the query to your personal query library. For more information, see [Manage your personal query library](../manage-your-personal-query-library).
* **Widget to Library**: For more information, see [Create XQL widgets](../../../monitor-dashboards-and-reports/advanced-configuration/create-custom-widgets/create-xql-widgets).

{% hint style="info" %}
### Tip

While the query is running, you can navigate away from the page. A notification is sent when the query has finished. You can also **Cancel** the query or run a new query, where you have the option to **Run only new query (cancel previous)** or **Run both queries**.
{% endhint %}

</details>
