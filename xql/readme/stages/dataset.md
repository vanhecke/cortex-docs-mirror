# dataset

Use the `dataset` stage to explicitly define the data table your XQL query will retrieve records from. This is a fundamental component used to specify the data source and is crucial for query optimization.

## Syntax

```sql
dataset [=] <dataset_name>
dataset in (<dataset_name1>, <dataset_name2>, ...)
cold_dataset = <dataset_name>
```

## Parameters

| Name           | Type     | Required | Description                                                                      |
| -------------- | -------- | -------- | -------------------------------------------------------------------------------- |
| `dataset_name` | string   | Yes      | The name of the dataset to query. If omitted, the query defaults to `xdr_data`.  |
| `in`           | operator | No       | An operator used to specify a list of multiple datasets to query simultaneously. |

## Returns

The `dataset` stage returns raw records and all available fields from the specified data source(s).

## Usage notes

* The `dataset` stage must always be the very first stage in your XQL query, unless it is preceded by a `config` stage.
* If you do not explicitly define a dataset, Cortex XDR/XSIAM will default to querying the `xdr_data` dataset.
* Dataset names in queries are always treated as if they are lowercase, even if you type them with uppercase characters (Case Insensitivity).
* Specifying the dataset early is a best practice for streamlining queries, as it helps reduce the amount of data processed.
* The `cold_dataset` syntax is used specifically for querying data stored in cold storage.

## Examples

### Example 1: Basic Dataset Specification

**Goal**: Explicitly specify a single data source for the query.

**XQL code**:

```sql
config timeframe = 1d // Set a practical timeframe for the query
| dataset = sample_xql_raw // Specifies the data source for the query
| limit 5 // Limits the number of returned records to improve performance
```

**Explanation**: This query retrieves all available fields from the `sample_xql_raw` dataset within the specified timeframe.

**Output**:

| event\_id | \_time                  | event\_description               |
| --------- | ----------------------- | -------------------------------- |
| 101       | 2023-10-26 10:00:00 UTC | "User login successful"          |
| 102       | 2023-10-26 10:05:30 UTC | "File access attempt"            |
| 103       | 2023-10-26 10:15:15 UTC | "Network connection established" |
| 104       | 2023-10-26 10:20:00 UTC | "System heartbeat"               |
| 105       | 2023-10-26 10:30:45 UTC | "Data transformation"            |

### Example 2: Specifying Multiple Datasets

**Goal**: Query across several different datasets using the `in` operator.

**XQL code**:

```sql
config timeframe = 1d // Ensures the query operates within a defined time window
| dataset in ("sample_xql_raw") // Specifies one or more datasets to query from
| filter is_successful = true // Filters for successful events
| fields event_id, event_description, is_successful // Selects only the necessary fields for output
| limit 5 // Prevents excessive results and improves query performance
```

**Explanation**: This query demonstrates the `dataset in` syntax. While `sample_xql_raw` is a single dataset, this syntax allows listing multiple datasets (for example, `dataset in ("dataset1", "dataset2")`) to aggregate results from multiple sources.

**Output**:

| event\_id | event\_description               | is\_successful |
| --------- | -------------------------------- | -------------- |
| 101       | "User login successful"          | true           |
| 103       | "Network connection established" | true           |
| 104       | "System heartbeat"               | true           |
| 105       | "Data transformation"            | true           |
| 107       | "Cloud resource modification"    | true           |

### Example 3: cold\_dataset Note (conceptual example)

**Goal**: Query data that is stored in cold storage.

**XQL code**:

```sql
config timeframe = 7d
| cold_dataset = sample_xql_raw_cold // Placeholder for a conceptual cold dataset
| limit 10
```

**Explanation**: The `cold_dataset = <dataset name>` syntax is used specifically for querying data stored in cold storage. This example conceptually queries a cold dataset named `sample_xql_raw_cold`.

**Output**:

| event\_id | \_time                  | event\_description               |
| --------- | ----------------------- | -------------------------------- |
| 101       | 2023-10-26 10:00:00 UTC | "User login successful"          |
| 102       | 2023-10-26 10:05:30 UTC | "File access attempt"            |
| 103       | 2023-10-26 10:15:15 UTC | "Network connection established" |

### Example 4: Default dataset (xdr\_data)

**Goal**: Implicitly query the default dataset (`xdr_data`) by omitting the `dataset` stage.

**XQL code**:

```sql
// This query implicitly uses the 'xdr_data' dataset
filter event_id = 101
| fields event_id, event_description
```

**Explanation**: If no `dataset` stage is explicitly defined, XQL queries automatically run against the `xdr_data` dataset. This example directly filters and selects fields, implicitly targeting the default dataset (represented here by `sample_xql_raw` data for context).

**Output**:

| event\_id | event\_description      |
| --------- | ----------------------- |
| 101       | "User login successful" |

## Related articles

* **Stages**: [`config`](config), [`filter`](filter), [`fields`](fields)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
