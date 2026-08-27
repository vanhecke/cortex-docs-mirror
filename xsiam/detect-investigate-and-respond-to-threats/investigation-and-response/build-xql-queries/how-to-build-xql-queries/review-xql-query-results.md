---
description: Review and analyze XQL query results in the Cortex XSIAM Query Builder.
---

# Review XQL query results

Review the following topics:

* [How to build XQL queries]()
* [Create XQL query](create-xql-query)

The results of a Cortex Query Language (XQL) query are displayed in the **Query Results** tab.

{% hint style="info" %}
### Note

It's also possible to graph the results displayed. For more information, see [Graph query results](graph-query-results).
{% endhint %}

### **Real-time query results**

Cortex XSIAM displays partial results for queries run in the Query Builder as they are received, subject to the limitations below. In a long-running query, viewing the initial findings enables you to refine, validate, or stop the query.

The partial results are displayed only in the **Table** tab. The results are added to the table as they are received in real time. The incremental query results aren't ordered, so they may not be in sequence.

{% hint style="info" %}
### Limitations

* Real time query results are available only in the Query Builder and in free text query.
* Real time results are displayed only for queries run on hot datasets.
* The Sort option is available only after all the data is retrieved.
* When you formulate complex queries, the results will be displayed when the query has finished running completely, and not in real time. Some of the clauses that are included in this restriction are:
  * JOIN - incremental results are supported only when the secondary dataset is smaller in size
  * SORT
  * COMP
  * WINDOWCOMP
  * TOP
{% endhint %}

{% hint style="info" %}
### Note

Results are received incrementally for the first 100K records, or up to 100MB worth of records, whichever comes first. After that, the next update is when the query has finished running completely.
{% endhint %}

<details>

<summary>Understanding the options available to investigate results</summary>

Use the following options in the **Query Results** tab to investigate your query results:

<table><thead><tr><th width="115">Option</th><th>Use</th></tr></thead><tbody><tr><td>Table tab</td><td><p>Displays results in rows and columns according to the entity ﬁelds. Columns can be filtered, using their filter icons.</p><p>More options (<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-5b092e4be32f608365073e2e4f47b91db519604b%2F8484899d72d2d609a169b230702a5e84e371d8c81725def9443d0ac9bc0c1d26.png?alt=media" alt="table-settings.png">) displays table layout options, which are divided into different sections:</p><ul><li>In the <strong>Appearance</strong> section, you can <strong>Show line breaks</strong> for any text field in the <strong>Query Results</strong>. By default, the text in these fields are wrapped unless the <strong>Show line breaks</strong> option is selected. In addition, you can change the way rows and columns are displayed.</li><li><p>In the <strong>Log Format</strong> section, you can change the way that logs are displayed:</p><ul><li><strong>RAW</strong>: Raw format of the entity in the database.</li><li><strong>JSON</strong>: Condensed JSON format with key value distinctions. NULL values are not displayed.</li><li><strong>TREE</strong>: Dynamic view of the JSON hierarchy with the option to collapse and expand the different hierarchies.</li></ul></li><li>In the <strong>Search column</strong> section, you can find a specific column; enable or disable display of columns using the checkboxes.</li></ul><p>Show and hide rows according to a specific field in a specific event: select a cell, right-click it, and then select either <strong>Show rows with …</strong> or <strong>Hide rows with …</strong></p></td></tr><tr><td>Graph tab</td><td>Use the <strong>Chart Editor</strong> to visualize the query results.</td></tr><tr><td>Advanced tab</td><td><p>Displays results in a table format which aggregates the entity ﬁelds into one column. You can change the layout, decide whether to <strong>Show line breaks</strong> for any text field in the results table, and change the log format from the <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-5b092e4be32f608365073e2e4f47b91db519604b%2F8484899d72d2d609a169b230702a5e84e371d8c81725def9443d0ac9bc0c1d26.png?alt=media" alt="table-settings.png"> menu.</p><p>Select <strong>Show more</strong> to pivot an <strong>Expanded View</strong> of the event results that include NULL values. You can toggle between the <strong>JSON</strong> and <strong>Tree</strong> views, search, and <strong>Copy to clipboard</strong>.</p></td></tr><tr><td>Export to File</td><td><p>Exports the results to a TSV (tab-separated values) ﬁle.</p><ul><li>More options (<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-5b092e4be32f608365073e2e4f47b91db519604b%2F8484899d72d2d609a169b230702a5e84e371d8c81725def9443d0ac9bc0c1d26.png?alt=media" alt="table-settings.png">) works in a similar way to how it works on the <strong>Table</strong> tab.</li><li><strong>Show more</strong> in the bottom left corner of each row opens the <strong>Expanded View</strong> of the event results that also include NULL values. Here, you can toggle between the <strong>JSON</strong> and <strong>Tree</strong> views, search, and <strong>Copy to clipboard</strong>.</li><li><p><strong>Log format</strong> options change the way that logs are displayed:</p><ul><li><strong>RAW</strong>: Raw format of the entity in the database.</li><li><strong>JSON</strong>: Condensed JSON format with key value distinctions. NULL values are not displayed.</li><li><strong>TREE</strong>: Dynamic view of the JSON hierarchy with the option to collapse and expand the diﬀerent hierarchies.</li></ul></li></ul></td></tr><tr><td>Refresh</td><td>Refreshes the query results.</td></tr><tr><td>Free text search</td><td>Searches the query results for text that you specify in the free text search. Click the <strong>Free text search</strong> icon to reveal or hide the free text search field.</td></tr><tr><td>Filter</td><td><p>Enables you to ﬁlter a particular ﬁeld in the interface that is displayed to specify your ﬁlter criteria.</p><p>For integer, boolean, and timestamp (such as <code>_time</code>) ﬁelds, we recommend that you use the <strong>Filter</strong> instead of the <strong>Free text</strong> search, in order to retrieve the most accurate query results.</p></td></tr><tr><td>Fields menu</td><td><p>Filters query results. To quickly set a ﬁlter, Cortex XSIAM displays the top ten results from which you can choose to build your ﬁlter. This option is only available in the <strong>Table</strong> and <strong>Advanced</strong> tabs,</p><p>From within the Fields menu, click on any ﬁeld (excluding JSON and array ﬁelds) to see a histogram of all the values found in the result set for that ﬁeld. This histogram includes:</p><ul><li>A count of the total number of times a value was found in the result set.</li><li>The value's frequency as a percentage of the total number of values found for the ﬁeld.</li><li>A bar chart showing the value's frequency.</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>In order for Cortex XSIAM to provide a histogram for a ﬁeld, the ﬁeld must not contain an array or a JSON object.</p></div></td></tr></tbody></table>

</details>

<details>

<summary>Available options for saving results</summary>

The Save As options save your query for future use:

* **Correlation Rule**: When compatible, saves the query as a Correlation Rule. For more information, see [What's a correlation rule?](../../../threat-management/detection-rules/what-are-detection-rules/whats-a-correlation-rule).
* **Query to Library**: Saves the query to your personal query library. For more information, see [personal query library](../manage-your-personal-query-library).
* **Widget to Library**

</details>

<details>

<summary>Investigating results in the Causality View or Timeline View</summary>

You can continue investigating the query results in the Causality View or Timeline by right-clicking the event and selecting the desired view. This option is available for the following types of events:

* Process (except for those with an event sub-type of termination)
* Network
* File
* Registry
* Injection
* Load image
* System calls
* Event logs for Windows
* System authentication logs for Linux

For network stories, you can pivot to the Causality View only. For cloud Cortex XSIAM events and Cloud Audit Logs, you can only pivot to the Cloud Causality View, while for software-as-a-service (SaaS) related issues for audit stories, such as Office 365 audit logs and normalized logs, you can only pivot to the SaaS Causality View.

</details>

<details>

<summary>Add file path to Malware Profile allowed list</summary>

Add a file path to your existing Malware Profile allowed list by right-clicking a \<path> field, such as **target\_process\_path**, and selecting **Add \<path type> to malware profile allow list**.

</details>
