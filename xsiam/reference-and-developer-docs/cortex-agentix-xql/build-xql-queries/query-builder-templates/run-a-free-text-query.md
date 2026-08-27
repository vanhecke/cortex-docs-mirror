---
description: Run free-text queries with Query Builder templates in Cortex XSIAM.
---

# Run a free text query

You can use the **Free text** template to query your datasets for free-text strings without building a Cortex Query Language (XQL) query. The template queries all of the raw datasets that are stored in your tenant and returns up to 1,000 results.

{% hint style="info" %}
### Note

The query in free-text search in the Query Templates page runs only on raw datasets. You can only scope your search using the search stage available in the XQL editor.\
Use the **`search`** stage in the XQL editor to use scoping to query free-text strings in specific datasets, normalized datasets, or all datasets in your tenant.
{% endhint %}

### How to run a free text query

1. Select **Investigation & Response** → **Query Templates**.
2. Under **General Search**, select **Free text**.
3. In the **Text Contains** field, type one or more strings. Separate multiple strings with pipes, which applies the OR operator.
4.  Click **TIME** and select a time frame for the query.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Free text search is limited to the last 90 days of data. Specifying a time frame outside of this limitation will cause the query to fail.</p></div>
5.  Click **Run** to start the query, or click **Schedule** to run the query at a specific time.

    Free text search searches the relevant columns in each dataset. Relevant columns are subject to a change and can vary between datasets.

    You can also click **Continue in XQL** to translate the query with the fields that you specified into XQL. In XQL you have the flexibility to add additional stages and functions that are not available in the Query Builder templates.
6.  Review the results.

    The searched string is highlighted in the results.

    In the **Fields** column, you can see all of the fields in which the string was discovered. Fields are listed in the following order: (1) `_time`, (2) `_dataset`, and (3) the fields in which the string was discovered, ordered by highest to lowest number of hits.

    In the `RAW_DATA` column, click **Show more** to see the specific row in the dataset in which the string was discovered.

### **What to do next**

* To edit or rerun the query, click **Back to edit** to review the template in the Query Builder, or **Continue in XQL** to review the XQL.
* Practice running queries with [Query Builder template examples](../../../../detect-investigate-and-respond-to-threats/investigation-and-response/build-xql-queries/query-builder-templates/query-builder-template-examples).
