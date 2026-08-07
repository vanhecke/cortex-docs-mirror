# min (comp)

Use the `min()` function to return the minimum value of a specified field across all rows in each group within the `comp` stage. This is equivalent to the SQL `MIN` aggregate function.

## Syntax

```sql
| comp min(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type                         | Required | Description                                                                                       |
| ------------- | ---------------------------- | -------- | ------------------------------------------------------------------------------------------------- |
| `field`       | numeric, string, or datetime | Yes      | The field from which to find the minimum value.                                                   |
| `group_field` | any                          | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.   |
| `alias`       | string                       | No       | An alias for the output field. If not specified, the output field name defaults to `min_<field>`. |

## Returns

**Type**: same as input field

**Description**: The `min()` function returns the minimum value found in the specified field within each group. Returns NULL if all values in the group are NULL.

## Usage notes

* **Data types**: The `min` function works with numeric, string, and datetime fields.
* **String comparison**: For string fields, the minimum is determined by lexicographic (alphabetical) ordering.
* **Null handling**: NULL values are ignored in the computation.
* **No grouping**: When used without a `by` clause, the function returns the minimum value across all rows.
* **Multiple aggregations**: Can be combined with other aggregation functions in the same `comp` stage.

## Examples

### Example 1: Find the earliest event time per host

**Goal**: Find the earliest event timestamp for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp min(_time) by agent_hostname as earliest_event
```

**Explanation**: The `min()` function finds the earliest `_time` value for each unique `agent_hostname`, returning the first event time per host.

**Output**:

| AGENT\_HOSTNAME | EARLIEST\_EVENT     |
| --------------- | ------------------- |
| workstation-1   | 2024-01-15 08:00:00 |
| workstation-2   | 2024-01-15 08:30:00 |

### Example 2: Find the minimum severity across all alerts

**Goal**: Find the lowest alert severity value across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp min(alert_severity) as lowest_severity
```

**Explanation**: Without a `by` clause, the `min()` function scans all rows and returns the single lowest `alert_severity` value.

**Output**:

| LOWEST\_SEVERITY |
| ---------------- |
| 1                |

### Example 3: Multiple aggregations in one comp stage

**Goal**: Find both the earliest and latest event times, plus total count, per host in a single query.

**XQL code**:

```sql
dataset = xdr_data
| comp min(_time) as earliest, max(_time) as latest, count(*) as total by agent_hostname
```

**Explanation**: This query combines `min()`, `max()`, and `count()` in a single `comp` stage to find the earliest and latest event timestamps along with the total event count for each `agent_hostname`.

**Output**:

| AGENT\_HOSTNAME | EARLIEST            | LATEST              | TOTAL |
| --------------- | ------------------- | ------------------- | ----- |
| workstation-1   | 2024-01-15 08:00:00 | 2024-01-15 14:30:00 | 25    |
| workstation-2   | 2024-01-15 08:30:00 | 2024-01-15 13:45:00 | 18    |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`max()`](max_with_comp_stage), [`min (windowcomp)`](min_with_windowcomp_stage), [`least()`](least)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
