---
description: Learn how to create Graph Search queries in Cortex XSIAM.
---

# Create Graph Search query

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

{% hint style="warning" %}
### Prerequisite

Graph Search requires **View** or **View/Edit** RBAC permissions for **Graph Search** under **Investigation & Response** → **Search**.
{% endhint %}

Review the following topics:

* [Get started with Graph Search queries](get-started-with-graph-search-queries)
* [How to build Graph Search queries?](how-to-build-graph-search-queries)
* [Understand Graph Search query results](understand-graph-search-query-results)
* [Graph Search examples](graph-search-examples)
* [Manage the Graph Search Query Library](manage-the-graph-search-query-library)

Build Graph Search queries to search your assets and findings by their relationship types and map them out in a unified and understandable view. You can build Graph Search queries using the built-in query interface embedded in the Query Builder.

1. Select **Investigation & Response** → **Search** → **Query Builder** → **Graph Search**.
2. From inside the Graph Search query interface at the top of the **Graph Search** page, click **Select** to open the entity picker dialog box.
3.  Choose the assets and findings nodes that you want to query.

    Keep in mind that multiple nodes are defined with an `OR` relationship between them. The top level node selection acts as the root of the query.
4.  To apply a condition to the assets or findings nodes that you've selected, click **WHERE**. Otherwise, skip to the next step.

    Select the applicable field (termed node attribute), operator, and value for the condition you want to define. The operators and values change according to the node attribute (field) that you select. At each level of the query, the relationship between node attribute conditions is `AND`. No other logical operator is available.
5. To define a relationship between the assets or findings nodes already selected and a new node, click **+**.
6. Define the **THAT** statement by selecting the new assets and findings nodes that you want to relate to the other nodes.
7. To apply a condition to the new asset and findings nodes that you've selected, repeat step **#4**.
8. Repeat steps **#5** to **#7** until you've finished building your query logic.
9.  When your query is complete, or at any time that you want to view the query results, click **Search**.

    The Graph Search results are displayed in a graph format by default. You can toggle to **Table** to view the results in a table format. In addition, you can export the graph results using the icon at the top of the page to a PNG, SVG, or TSV file.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><ul><li>After running the query, you can view the complete query by hovering over the last <strong>THAT...</strong> in the Graph Search query interface, and the query is displayed in a tooltip.</li><li>If your query doesn't find any results or you want to change your query for any reason, you can always click anywhere in the Graph Search query interface, where your existing query is defined, to display the complete query, update your query, and rerun the search.</li></ul></div>
10. You can save your query to the Query Library by clicking **Save Query**.

    1. Set these parameters:
       * **Query Name**: Specify a unique name for the Graph Search query. Query names must be unique in both private and shared lists, which includes other people’s queries.
       * **Query Description** (Optional): Specify a descriptive name for your Graph Search query.
       * **Labels** (Optional): Specify a label that is associated with your Graph Search query. You can add a label and then select **Create Label**, or select a label from the list, if any exist from a previous query. Adding a label to your Graph Search query enables you to search for queries using this label in the Query Library.
       * **Share with others**: You can either set the Graph Search query to be private and only accessible by you (default) or move the toggle to **Share with others** the query, so that other users using the same tenant can access the query in their Query Library.
    2.  Click **Save**.

        A notification appears confirming that the query was saved successfully to the library, and closes on its own after a few seconds.

        The Graph Search query that you added is now listed as the first entry in the **Query Library**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>For more information about the Query Library, see <a href="manage-the-graph-search-query-library">Manage the Graph Search Query Library</a>.</p></div>
