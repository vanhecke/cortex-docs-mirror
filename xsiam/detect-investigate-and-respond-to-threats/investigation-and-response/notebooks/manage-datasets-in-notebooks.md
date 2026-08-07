# Manage datasets in Notebooks

Create, edit, and delete datasets directly in Notebooks and use them in rules.

You can create datasets in BigQuery through Notebooks using custom Cortex XSIAM APIs. You can then bring the insights and enriched data through machine learning into Cortex XSIAM to use them inside rules. For example, you can run a query in Cortex XSIAM that searches a case and correlates it to a sensitive users list you've created in Notebooks to trigger an issue.

To use the Cortex XSIAM APIs inside Notebooks, in **Investigation & Response** → **Notebooks**, import them from the Cortex SDK.

```programlisting
from cortex.dataset import define_dataset, create_dataset_from_dataframe, delete_dataset, get_created_datasets. 
from cortex.xql import start_query, get_query_results.
```

The created datasets are available for querying in the **Query Builder** and can be used when defining rules. You can view them under **Dataset Management**, and they can be selected for access when creating a user role. Creating and deleting datasets are recorded in the **Management Audit Logs**.

To change the schema of a dataset created using the Notebooks API, delete the dataset and create a new dataset with the updated schema.

You can use all the Google BigQuery functions to update the data in a dataset created using the Notebooks API.

The functions that are available for creating and editing datasets in Notebooks are listed below.

<details>

<summary>Define dataset</summary>

Creates an XQL dataset based on an existing BQ table.

```programlisting
define_dataset(table_name: str, client: Optional[Client] = None)
```

|           |                                                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Arguments | <ul><li><code>table_name</code>: Existing BQ table name created by the user.</li><li><code>client</code>: Cortex HTTP client.</li></ul> |

</details>

<details>

<summary>Create a dataset from a dataframe</summary>

Creates an XQL dataset and the table at the same time, where you supply the data and the schema of the table in the API.

```programlisting
create_dataset_from_dataframe(
    table_name: str,
    dataframe: DataFrame,
    schema: Optional[Sequence[Union[SchemaField, Mapping[str, Any]]]] = None,
    client: Optional[Client] = None,
    bq_client: Optional[BqClient] = None,
)
```

<table><thead><tr><th width="111.00006103515625"></th><th></th></tr></thead><tbody><tr><td>Arguments</td><td><ul><li><code>table_name</code>: Dataset name.</li><li><p><code>schema</code>: Schema of the table - a list of <code>dicts</code> or <code>SchemaField</code> objects defining the structure of the table.</p><p>For example:</p><p><code>schema = [ SchemaField("project_name", "STRING"), SchemaField("project_id", "INT64"), SchemaField("users", "STRING", mode="REPEATED"), SchemaField("assets", "RECORD", mode="REPEATED", fields=[ SchemaField("ip", "STRING"), SchemaField("created_time", "TIMESTAMP") ]) ]</code></p></li><li><code>client</code>: Cortex HTTP client.</li><li><code>bq_client</code>: Cortex BigQuery client.</li></ul></td></tr></tbody></table>

{% hint style="info" %}
If a schema is not provided, the function automatically detects the schema.
{% endhint %}

</details>

<details>

<summary>Get created datasets</summary>

Retrieves a list of all XQL datasets generated using the Cortex SDK.

```programlisting
get_created_datasets(client: Optional[Client] = None)
```

<table><thead><tr><th width="131"></th><th></th></tr></thead><tbody><tr><td>Arguments</td><td><code>client</code>: Cortex HTTP client.</td></tr></tbody></table>

</details>

<details>

<summary>Delete dataset</summary>

Deletes the XQL dataset that was created by the Cortex SDK.

{% hint style="info" %}
* Using this function, you can only delete datasets created using the Notebooks APIs.
* When you delete a dataset, the rules that use the dataset return an error.
{% endhint %}

```programlisting
delete_dataset(dataset_name: str, delete_underlying_bq_table: Optional[bool] = False, client: Optional[Client] = None)
```

<table><thead><tr><th width="126"></th><th></th></tr></thead><tbody><tr><td>Arguments</td><td><ul><li><code>dataset_name</code>: Name of the dataset to be deleted.</li><li><code>delete_underlying_bq_table</code>: When True, deletes the BQ table related to the dataset. Default value is False.</li><li><code>client</code>: Cortex HTTP client.</li></ul></td></tr></tbody></table>

</details>
