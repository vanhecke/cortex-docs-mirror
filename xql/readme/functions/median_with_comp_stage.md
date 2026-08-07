# median (comp)

Use the `median()` function to return the median (middle value) of a specified numeric field across all rows in each group within the `comp` stage. For an even number of values, it returns the average of the two middle values. This is equivalent to computing the 50th percentile.

## Syntax

```sql
| comp median(<field>) [by <group_field1>, <group_field2>, ...] [as <alias>]
```

## Parameters

| Name          | Type    | Required | Description                                                                                          |
| ------------- | ------- | -------- | ---------------------------------------------------------------------------------------------------- |
| `field`       | numeric | Yes      | The numeric field from which to compute the median value.                                            |
| `group_field` | any     | No       | One or more fields to group the results by. If omitted, all rows are treated as a single group.      |
| `alias`       | string  | No       | An alias for the output field. If not specified, the output field name defaults to `median_<field>`. |

## Returns

**Type**: numeric (float)

**Description**: The `median()` function returns the median value of the specified field within each group. Returns NULL if all values in the group are NULL.

## Usage notes

* **Numeric only**: The `median` function only works with numeric fields.
* **Null handling**: NULL values are ignored in the computation.
* **Odd count**: For an odd number of non-NULL values, the median is the middle value when sorted.
* **Even count**: For an even number of non-NULL values, the median is the average of the two middle values.
* **Return type**: The result is always returned as a floating-point number.
* **No grouping**: When used without a `by` clause, the function computes the median across all rows.

## Examples

### Example 1: Median response time per endpoint

**Goal**: Compute the median response time for each host.

**XQL code**:

```sql
dataset = xdr_data
| comp median(action_total_time) by agent_hostname as median_response_time
```

**Explanation**: The `median()` function computes the middle value of `action_total_time` for each unique `agent_hostname`, providing a representative response time that is less affected by outliers than the average.

**Output**:

| AGENT\_HOSTNAME | MEDIAN\_RESPONSE\_TIME |
| --------------- | ---------------------- |
| workstation-1   | 45.5                   |
| workstation-2   | 32.0                   |

### Example 2: Overall median of bytes received

**Goal**: Compute the overall median of bytes received across all events.

**XQL code**:

```sql
dataset = xdr_data
| comp median(action_network_bytes_received) as median_bytes
```

**Explanation**: Without a `by` clause, the `median()` function computes the median of `action_network_bytes_received` across all rows, returning a single value.

**Output**:

| MEDIAN\_BYTES |
| ------------- |
| 1024.5        |

## Related articles

* **Stages**: [`comp`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`median (windowcomp)`](median_with_windowcomp_stage), [`avg()`](avg_with_comp_stage), [`max()`](max_with_comp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
