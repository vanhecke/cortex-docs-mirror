# sum (comp)

Use the `sum()` function to compute the sum of all values of a specified numeric field across all rows in each group within the `comp` stage. This is equivalent to the SQL `SUM` aggregate function.

## Syntax

```sql
| comp sum(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type    | Required | Description                                                                                       |
| ------------- | ------- | -------- | ------------------------------------------------------------------------------------------------- |
| `field`       | numeric | Yes      | The numeric field whose values will be summed.                                                    |
| `group_field` | any     | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.   |
| `alias`       | string  | No       | An alias for the output field. If not specified, the output field name defaults to `sum_<field>`. |

## Returns

**Type**: numeric

**Description**: The `sum()` function returns the total sum of all non-NULL values of the specified field within each group. Returns NULL if all values in the group are NULL. Returns 0 if the group is empty.

## Usage notes

* **Data types**: The `sum` function only works with numeric fields.
* **Null handling**: NULL values are ignored in the computation.
* **No grouping**: When used without a `by` clause, the function returns the sum across all rows.
* **Multiple aggregations**: Can be combined with other aggregation functions in the same `comp` stage.
* **Overflow**: For very large datasets with large values, be aware of potential numeric overflow.

## Examples

### Example 1: Total bytes sent per host

**Goal**: Compute the total bytes sent for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp sum(bytes_sent) by agent_hostname as total_bytes_sent
```

**Explanation**: The `sum()` function adds up all `bytes_sent` values for each unique `agent_hostname`, returning the total bytes sent per host.

**Output**:

| AGENT\_HOSTNAME | TOTAL\_BYTES\_SENT |
| --------------- | ------------------ |
| workstation-1   | 1048576            |
| workstation-2   | 524288             |

### Example 2: Total events across all data

**Goal**: Compute the total sum of alert severities across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp sum(alert_severity) as total_severity
```

**Explanation**: Without a `by` clause, the `sum()` function computes the total of all `alert_severity` values across the entire dataset.

**Output**:

| TOTAL\_SEVERITY |
| --------------- |
| 342             |

### Example 3: Sum with multiple aggregations

**Goal**: Compute total bytes sent and received along with event count per host.

**XQL code**:

```sql
dataset = xdr_data
| comp sum(bytes_sent) as total_sent, sum(action_network_bytes_received) as total_received, count(*) as event_count by agent_hostname
```

**Explanation**: This query combines multiple `sum()` calls with `count()` in a single `comp` stage to provide a comprehensive traffic summary per host.

**Output**:

| AGENT\_HOSTNAME | TOTAL\_SENT | TOTAL\_RECEIVED | EVENT\_COUNT |
| --------------- | ----------- | --------------- | ------------ |
| workstation-1   | 1048576     | 2097152         | 150          |
| workstation-2   | 524288      | 1048576         | 85           |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`sum (windowcomp)`](sum_with_windowcomp_stage), [`count()`](count_with_comp_stage), [`avg()`](avg_with_comp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
