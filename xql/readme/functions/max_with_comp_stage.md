# max (comp)

Use the `max()` function to return the maximum value of a specified field across all rows in each group within the `comp` stage. This is equivalent to the SQL `MAX` aggregate function.

## Syntax

```sql
| comp max(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type                         | Required | Description                                                                                       |
| ------------- | ---------------------------- | -------- | ------------------------------------------------------------------------------------------------- |
| `field`       | numeric, string, or datetime | Yes      | The field from which to find the maximum value.                                                   |
| `group_field` | any                          | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.   |
| `alias`       | string                       | No       | An alias for the output field. If not specified, the output field name defaults to `max_<field>`. |

## Returns

**Type**: same as input field

**Description**: The `max()` function returns the maximum value found in the specified field within each group. Returns NULL if all values in the group are NULL.

## Usage notes

* **Data types**: The `max` function works with numeric, string, and datetime fields.
* **String comparison**: For string fields, the maximum is determined by lexicographic (alphabetical) ordering.
* **Null handling**: NULL values are ignored in the computation.
* **No grouping**: When used without a `by` clause, the function returns the maximum value across all rows.
* **Multiple aggregations**: Can be combined with other aggregation functions in the same `comp` stage.

## Examples

### Example 1: Find the latest event time per host

**Goal**: Find the most recent event timestamp for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp max(_time) by agent_hostname as latest_event
```

**Explanation**: The `max()` function finds the latest `_time` value for each unique `agent_hostname`, returning the most recent event time per host.

**Output**:

| AGENT\_HOSTNAME | LATEST\_EVENT       |
| --------------- | ------------------- |
| workstation-1   | 2024-01-15 14:30:00 |
| workstation-2   | 2024-01-15 13:45:00 |

### Example 2: Find the maximum severity across all alerts

**Goal**: Find the highest alert severity value across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp max(alert_severity) as highest_severity
```

**Explanation**: Without a `by` clause, the `max()` function scans all rows and returns the single highest `alert_severity` value.

**Output**:

| HIGHEST\_SEVERITY |
| ----------------- |
| 10                |

### Example 3: Multiple aggregations in one comp stage

**Goal**: Find both the latest and earliest event times per host in a single query.

**XQL code**:

```sql
dataset = xdr_data
| comp max(_time) as latest, min(_time) as earliest by agent_hostname
```

**Explanation**: This query combines `max()` and `min()` in a single `comp` stage to find both the latest and earliest event timestamps for each `agent_hostname`.

**Output**:

| AGENT\_HOSTNAME | LATEST              | EARLIEST            |
| --------------- | ------------------- | ------------------- |
| workstation-1   | 2024-01-15 14:30:00 | 2024-01-15 08:00:00 |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`min()`](min_with_comp_stage), [`max (windowcomp)`](max_with_windowcomp_stage), [`greatest()`](greatest)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
