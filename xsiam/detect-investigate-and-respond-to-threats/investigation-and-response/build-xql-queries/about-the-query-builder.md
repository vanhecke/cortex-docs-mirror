# About the Query Builder

The Query Builder aids in the detection of threats by allowing you to search for indicators of compromise and suspicious patterns within data sources. It assists in expanding case investigations by identifying related events and entities, such as activities associated with specific user accounts or network lateral movement. In addition, the Query Builder enables data analytics on suspected threats, helping organizations analyze large volumes of data to identify trends, anomalies, and correlations that may indicate potential security issues.

To support investigation and analysis, you can search all of the data ingested by Cortex XSIAM by creating queries in the Query Builder. You can create queries that investigate leads, expose the root cause of an issue, perform damage assessment, and hunt for threats from your data sources.

Cortex XSIAM provides different options in the Query Builder for creating queries:

*   XQL (Build your own queries)

    You can use the Cortex Query Language (XQL) to build complex and flexible queries that search specific datasets or presets, or the entire Cortex Data Model (XDM). With XQL Search, you create queries based on stages, functions, and operators. To help you build your queries, Cortex XSIAM provides tools in the interface that provide suggestions as you type, or you can look up predefined queries, common stages and examples. For more information, see [How to build XQL queries](how-to-build-xql-queries).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Schema changes to datasets may not be reflected in the autocomplete suggestions and deﬁnitions as you type in real time the XQL query, and can appear with a slight delay.</p></div>

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>When creating XQL queries, you can:</p><ul><li>Use the up and down arrow keys to navigate through the auto-suggestion commands and definitions.</li><li>Select an auto-suggestion command by pressing either the <strong>Enter</strong> or <strong>Tab</strong> key.</li><li>Press <strong>Shift</strong>+<strong>Enter</strong> to add a new line, and easily ignore the auto-suggestion output.</li><li>Close the auto-suggestion output by pressing the <strong>Esc</strong> key.</li></ul></div>
*   Query Builder templates (No XQL knowledge required)

    You can use the Query Builder templates to access your data without prior XQL knowledge. The templates include predefined filtering fields and key fieldsets, and can include any field from the XDM schema.

    As the templates are also based on XQL, you can also translate your template queries into XQL. With this flexibility, you can enrich the basic queries created by templates for more detailed investigation, or use the templates as a starting point for creating complex queries with full XQL functionality. For more information, see [Query Builder templates](query-builder-templates).
* Graph Search to build queries to search assets, findings, and their contextual data. For more information, see [How to build Graph Search queries?](../../../reference-and-developer-docs/graph-search/how-to-build-graph-search-queries).

{% hint style="info" %}
### Tip

If you prefer to use the Query Builder in **Legacy mode**, switch the toggle in the header. In Legacy mode, the Query Builder searches predefined datasets only. To search the full XDM Data Model, switch to **New mode** or select **XQL Search**.
{% endhint %}
