# approx\_count

Use the `approx_count()` function to calculate an approximate count of distinct values in a specified field.

## Syntax

```sql
approx_count(<field>)
```

## Parameters

| Name    | Type   | Required | Description                                                        |
| ------- | ------ | -------- | ------------------------------------------------------------------ |
| `field` | string | Yes      | The name of the field for which you want to count distinct values. |

## Returns

The `approx_count()` function returns a single approximate integer value representing the number of distinct values found in the specified field.

## Usage notes

* The `approx_count()` function is an approximate aggregate function. The function is designed to be more scalable in terms of memory usage and processing time compared to exact aggregate functions like `count_distinct()`, especially for large datasets.
* This function must be used with the `comp` stage.
* You can use the `by` clause in the `comp` stage to partition the data into groups, allowing `approx_count()` to compute the approximate distinct count independently for each group.
* You can use the `addrawdata = true` option in the `comp` stage to include a column listing the raw data events that contributed to the aggregate result.

## Examples

### Example 1: Calculate approximate distinct count across the entire dataset

**Goal**: Calculate the approximate number of unique `event_description` values for all records in the dataset.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| comp approx_count(event_description) as unique_event_descriptions
```

**Explanation**: This query computes the approximate number of unique `event_description` values present in the `sample_xql_raw` dataset and names the resulting field `unique_event_descriptions`.

**Output**:

| unique\_event\_descriptions |
| --------------------------- |
| 10                          |

### Example 2: Calculate approximate distinct count grouped by another field

**Goal**: Calculate the approximate number of unique `dst_domain` values separately for successful and unsuccessful events.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| comp approx_count(dst_domain) as unique_domains_by_status by is_successful

```

**Explanation**: The query groups records by their `is_successful` status and then calculates the approximate number of unique `dst_domain` values for each group, presenting the counts in the `unique_domains_by_status` field.

**Output**:

| is\_successful | unique\_domains\_by\_status |
| -------------- | --------------------------- |
| true           | 7                           |
| false          | 3                           |

### Example 3: Calculate approximate distinct count with raw data inclusion

**Goal**: Calculate the approximate distinct count of `event_description` grouped by `is_successful` and include the raw events that contributed to the calculation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| comp approx_count(event_description) as unique_descriptions_by_status by is_successful addrawdata = true as raw_events_for_distinct_count

```

**Explanation**: This query calculates the approximate distinct count of `event_description` grouped by `is_successful`. Additionally, `addrawdata = true` generates a new column named `raw_events_for_distinct_count`, which contains a JSON representation of the raw events that contributed to each computed approximate distinct count.

**Output**:

| is\_successful | unique\_descriptions\_by\_status | raw\_events\_for\_distinct\_count                                                                                                                               |
| -------------- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| true           | 7                                | \[{"event\_id": 101, "event\_description": "User login successful", ...}, {"event\_id": 103, "event\_description": "Network connection established", ...}, ...] |
| false          | 3                                | \[{"event\_id": 102, "event\_description": "File access attempt", ...}, {"event\_id": 106, "event\_description": "Unauthorized access detected", ...}, ...]     |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`config`](../stages/comp), [`limit`](../stages/limit)
* **Functions**: [`approx_quantiles`](approx_quantiles), [`approx_top`](approx_top), [`count_distinct`](count_distinct)
