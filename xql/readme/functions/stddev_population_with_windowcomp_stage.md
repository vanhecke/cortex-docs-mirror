# stddev\_population (windowcomp)

Use the `stddev_population()` function within the `windowcomp` stage to compute the population standard deviation of a specified numeric field over a window of rows. Unlike the `comp` stage version, the `windowcomp` version preserves all original rows and adds the computed standard deviation as a new field. This is equivalent to `STDDEV_POP() OVER(...)` in SQL.

## Syntax

```sql
| windowcomp stddev_population(<field>) [by <partition_field1>, <partition_field2>, ...] [sort [asc|desc] <sort_field1>, ...] [between <lower> [and <upper>] [frame_type=rows|range]] [as <alias>]
```

## Parameters

| Name              | Type              | Required | Description                                                                                                           |
| ----------------- | ----------------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `field`           | numeric           | Yes      | The numeric field from which to compute the population standard deviation.                                            |
| `partition_field` | any               | No       | One or more fields to partition the data by (equivalent to SQL `PARTITION BY`).                                       |
| `sort_field`      | any               | No       | One or more fields to define the order within each partition (equivalent to SQL `ORDER BY`). Defaults to ascending.   |
| `lower`           | integer or `null` | No       | Lower bound of the window frame. `0` = current row, negative = rows before, `null` = unbounded.                       |
| `upper`           | integer or `null` | No       | Upper bound of the window frame. `0` = current row, positive = rows after, `null` = unbounded.                        |
| `frame_type`      | `rows` or `range` | No       | Type of window frame. `rows` (default) uses physical row offsets; `range` uses value-based offsets on the sort field. |
| `alias`           | string            | No       | An alias for the output field.                                                                                        |

## Returns

**Type**: numeric (float)

**Description**: The `stddev_population()` function returns the population standard deviation within the defined window for each row. All original rows are preserved.

## Usage notes

* **Row preservation**: Unlike `comp stddev_population()`, the `windowcomp` version does not reduce the number of rows.
* **Default frame**: If no window frame is specified, the default frame is from the start of the partition to the current row (`between null and 0`).
* **Null handling**: NULL values are ignored in the computation.
* **Running standard deviation**: Can be combined with `sort` to compute a running population standard deviation.
* **Population vs. sample**: Use `stddev_population()` for the entire population; use `stddev_sample()` for a sample.

## Examples

### Example 1: Population standard deviation per host (all rows preserved)

**Goal**: Compute the population standard deviation of response times for each host while preserving all rows.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp stddev_population(action_total_time) by agent_hostname as stddev_per_host
```

**Explanation**: The `stddev_population()` function computes the population standard deviation of `action_total_time` within each `agent_hostname` partition. All original rows are preserved.

**Output**:

| \_TIME              | AGENT\_HOSTNAME | ACTION\_TOTAL\_TIME | STDDEV\_PER\_HOST |
| ------------------- | --------------- | ------------------- | ----------------- |
| 2024-01-15 08:00:00 | workstation-1   | 50                  | 16.33             |
| 2024-01-15 09:00:00 | workstation-1   | 30                  | 16.33             |
| 2024-01-15 10:00:00 | workstation-1   | 70                  | 16.33             |
| 2024-01-15 08:30:00 | workstation-2   | 40                  | 5.00              |
| 2024-01-15 09:30:00 | workstation-2   | 50                  | 5.00              |

### Example 2: Running standard deviation over time

**Goal**: Compute a running population standard deviation of bytes received, ordered by time.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp stddev_population(action_network_bytes_received) sort asc _time as running_stddev
```

**Explanation**: By sorting on `_time`, the function computes a running population standard deviation from the start of the dataset up to the current row.

**Output**:

| \_TIME              | ACTION\_NETWORK\_BYTES\_RECEIVED | RUNNING\_STDDEV |
| ------------------- | -------------------------------- | --------------- |
| 2024-01-15 08:00:00 | 500                              | 0.00            |
| 2024-01-15 09:00:00 | 250                              | 125.00          |
| 2024-01-15 10:00:00 | 400                              | 102.14          |
| 2024-01-15 11:00:00 | 100                              | 147.90          |

### Example 3: Standard deviation within a sliding window

**Goal**: Compute the population standard deviation within a sliding window of 5 rows.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp stddev_population(action_total_time) sort asc _time between -2 and 2 as sliding_stddev
```

**Explanation**: The `between -2 and 2` clause defines a sliding window of up to 5 rows centered on the current row. The function computes the population standard deviation within that window.

**Output**:

| \_TIME              | ACTION\_TOTAL\_TIME | SLIDING\_STDDEV |
| ------------------- | ------------------- | --------------- |
| 2024-01-15 08:00:00 | 50                  | 12.47           |
| 2024-01-15 09:00:00 | 30                  | 14.79           |
| 2024-01-15 10:00:00 | 70                  | 16.33           |
| 2024-01-15 11:00:00 | 40                  | 14.14           |

## Related articles

* **Stages**: [`windowcomp`](../stages/windowcomp), [`comp`](../stages/comp), [`sort`](../stages/sort)
* **Functions**: [`stddev_population (comp)`](stddev_population_with_comp_stage), [`stddev_sample()`](stddev_sample_with_windowcomp_stage), [`avg()`](avg_with_windowcomp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
