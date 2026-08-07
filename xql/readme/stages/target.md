# target

Use the `target` stage to persist the results of your query to a new or existing dataset or lookup table. This allows the results to be used in subsequent queries, facilitating complex data pipelines and long-term storage.

## Syntax

```sql
target type=dataset|lookup [append=true|false] <dataset name>
```

## Parameters

| Name           | Type    | Required | Description                                                                                                                                   |
| -------------- | ------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`         | string  | Yes      | Defines the kind of storage for your query results. Supported values are `dataset` (persistent storage) or `lookup` (small reference tables). |
| `append`       | boolean | No       | Controls how results are added to an existing dataset or lookup table. `true` appends results; `false` (default) overwrites existing data.    |
| `dataset name` | string  | Yes      | A unique name for your new or existing dataset or lookup table.                                                                               |

## Returns

The `target` stage persists the query results to the specified storage destination (dataset or lookup table) and allows them to be referenced in future queries.

## Usage notes

* The `target` stage **must** be the final stage in your XQL query. You cannot place any other stages after it.
* Datasets created via the `target` stage are persistent and can be queried later using the standard `dataset = <dataset name>` syntax.
* For very long time windows or complex operations, running multiple smaller queries and appending their results to a working dataset using `target type=dataset append=true` can significantly outperform a single, long-running query.
* Be mindful of the size limit for `lookup` tables, which is 50 MB (or 30 MB if uploaded via the Dataset Management page).

## Examples

### Example 1: Create new dataset (implicit append)

**Goal**: Save all successful login events to a new dataset called `my_successful_logins`.

**XQL code**:

```sql
dataset = sample_xql_raw
| filter event_description = "User login successful" and is_successful = true
| fields event_id, event_description, _time
| target type=dataset my_successful_logins
```

**Explanation**: The query filters the `sample_xql_raw` dataset for successful user logins and saves the selected fields to a new persistent dataset named `my_successful_logins`. Since `append` is not specified, it defaults to `false` (overwrite) behavior when creating new, but functionally acts as a creation step.

**Output**:

| event\_id | event\_description      | \_time                  |
| --------- | ----------------------- | ----------------------- |
| 101       | "User login successful" | 2023-10-26 10:00:00 UTC |

### Example 2: Explicitly creating a new dataset (append=false)

**Goal**: Save network connection durations to a dataset named `event_durations_summary`, explicitly overwriting any existing data.

**XQL code**:

```sql
dataset = sample_xql_raw
| filter event_description = "Network connection established"
| fields event_id, duration_seconds, _time
| target type=dataset append=false event_durations_summary
```

**Explanation**: This query filters for network connection events and saves them to `event_durations_summary`. The `append=false` parameter ensures that if this dataset already exists, its previous content is completely overwritten with these new results.

**Output**:

| event\_id | duration\_seconds | \_time                  |
| --------- | ----------------- | ----------------------- |
| 103       | 10.2              | 2023-10-26 10:15:15 UTC |

### Example 3: Appending to an existing dataset (append=true)

**Goal**: Append "Database backup completed" events to the previously created `my_successful_logins` dataset.

**XQL code**:

```sql
dataset = sample_xql_raw
| filter event_description = "Database backup completed" and is_successful = true
| fields event_id, event_description, _time
| target type=dataset append=true my_successful_logins
```

**Explanation**: This query filters for successful database backup events. The `append=true` parameter appends these new records to the existing `my_successful_logins` dataset (created in Example 1) instead of overwriting it.

**Output**:

| event\_id | event\_description          | \_time                  |
| --------- | --------------------------- | ----------------------- |
| 101       | "User login successful"     | 2023-10-26 10:00:00 UTC |
| 110       | "Database backup completed" | 2023-10-26 11:00:10 UTC |

### Example 4: Creating a lookup table (type=lookup)

**Goal**: Create a small lookup table named `event_codes_lookup` containing `event_id` and extracted status codes.

**XQL code**:

```sql
dataset = sample_xql_raw
| alter status_code = to_number(json_extract_scalar(simple_json_data, "$.code"))
| filter status_code != null
| fields event_id, status_code
| target type=lookup event_codes_lookup
```

**Explanation**: The query extracts status codes from the JSON data, filters out nulls, and saves the `event_id` and `status_code` mapping to a lookup table named `event_codes_lookup`. Lookup tables are optimized for small, static reference data.

**Output**:

| event\_id | status\_code |
| --------- | ------------ |
| 101       | 200          |
| 109       | 429          |

## Related articles

* **Stages**: [`dataset`](dataset), [`filter`](filter), [`fields`](fields), [`alter`](alter)
* **Functions**: [`json_extract_scalar`](../functions/json_extract_scalar), [`to_number`](../functions/to_number)
