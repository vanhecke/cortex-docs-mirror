# stddev\_sample (windowcomp)

Use the `stddev_sample()` function within the `windowcomp` stage to compute the sample standard deviation of a specified numeric field over a window of rows. Unlike the `comp` stage version, the `windowcomp` version preserves all original rows and adds the computed sample standard deviation as a new field. This is equivalent to `STDDEV_SAMP() OVER(...)` in SQL.

## Syntax

```sql
| windowcomp stddev_sample(<field>) [by <partition_field1>, <partition_field2>, ...] [sort [asc|desc] <sort_field1>, ...] [between <lower> [and <upper>] [frame_type=rows|range]] [as <alias>]
```

## Parameters

| Name              | Type              | Required | Description                                                                                                           |
| ----------------- | ----------------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `field`           | numeric           | Yes      | The numeric field from which to compute the sample standard deviation.                                                |
| `partition_field` | any               | No       | One or more fields to partition the data by (equivalent to SQL `PARTITION BY`).                                       |
| `sort_field`      | any               | No       | One or more fields to define the order within each partition (equivalent to SQL `ORDER BY`). Defaults to ascending.   |
| `lower`           | integer or `null` | No       | Lower bound of the window frame. `0` = current row, negative = rows before, `null` = unbounded.                       |
| `upper`           | integer or `null` | No       | Upper bound of the window frame. `0` = current row, positive = rows after, `null` = unbounded.                        |
| `frame_type`      | `rows` or `range` | No       | Type of window frame. `rows` (default) uses physical row offsets; `range` uses value-based offsets on the sort field. |
| `alias`           | string            | No       | An alias for the output field.                                                                                        |

## Returns

**Type**: numeric (float)

**Description**: The `stddev_sample()` function returns the sample standard deviation (using Bessel's correction, N-1) within the defined window for each row. All original rows are preserved. Returns NULL when the window contains fewer than two non-NULL values.

## Usage notes

* **Row preservation**: Unlike `comp stddev_sample()`, the `windowcomp` version does not reduce the number of rows.
* **Bessel's correction**: Uses N-1 in the denominator for unbiased estimation from a sample.
* **Default frame**: If no window frame is specified, the default frame is from the start of the partition to the current row (`between null and 0`).
* **Null handling**: NULL values are ignored in the computation.
* **Minimum values**: Requires at least two non-NULL values in the window to produce a result.
* **Running standard deviation**: Can be combined with `sort` to compute a running sample standard deviation.

## Examples

### Example 1: Sample standard deviation per host (all rows preserved)

**Goal**: Compute the sample standard deviation of response times for each host while preserving all rows.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp stddev_sample(action_total_time) by agent_hostname as sample_stddev_per_host
```

**Explanation**: The `stddev_sample()` function computes the sample standard deviation of `action_total_time` within each `agent_hostname` partition using Bessel's correction. All original rows are preserved.

**Output**:

| \_TIME              | AGENT\_HOSTNAME | ACTION\_TOTAL\_TIME | SAMPLE\_STDDEV\_PER\_HOST |
| ------------------- | --------------- | ------------------- | ------------------------- |
| 2024-01-15 08:00:00 | workstation-1   | 50                  | 20.00                     |
| 2024-01-15 09:00:00 | workstation-1   | 30                  | 20.00                     |
| 2024-01-15 10:00:00 | workstation-1   | 70                  | 20.00                     |
| 2024-01-15 08:30:00 | workstation-2   | 40                  | 7.07                      |
| 2024-01-15 09:30:00 | workstation-2   | 50                  | 7.07                      |

### Example 2: Running sample standard deviation over time

**Goal**: Compute a running sample standard deviation of bytes received, ordered by time.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp stddev_sample(action_network_bytes_received) sort asc _time as running_sample_stddev
```

**Explanation**: By sorting on `_time`, the function computes a running sample standard deviation from the start of the dataset up to the current row. The first row returns NULL because at least two values are needed.

**Output**:

| \_TIME              | ACTION\_NETWORK\_BYTES\_RECEIVED | RUNNING\_SAMPLE\_STDDEV |
| ------------------- | -------------------------------- | ----------------------- |
| 2024-01-15 08:00:00 | 500                              | null                    |
| 2024-01-15 09:00:00 | 250                              | 176.78                  |
| 2024-01-15 10:00:00 | 400                              | 125.83                  |
| 2024-01-15 11:00:00 | 100                              | 170.78                  |

### Example 3: Sample standard deviation within a sliding window

**Goal**: Compute the sample standard deviation within a sliding window of 3 rows.

**XQL code**:

```sql
dataset = xdr_data
| windowcomp stddev_sample(action_total_time) sort asc _time between -1 and 1 as sliding_sample_stddev
```

**Explanation**: The `between -1 and 1` clause defines a sliding window of up to 3 rows centered on the current row. The function computes the sample standard deviation within that window using Bessel's correction.

**Output**:

| \_TIME              | ACTION\_TOTAL\_TIME | SLIDING\_SAMPLE\_STDDEV |
| ------------------- | ------------------- | ----------------------- |
| 2024-01-15 08:00:00 | 50                  | 14.14                   |
| 2024-01-15 09:00:00 | 30                  | 20.00                   |
| 2024-01-15 10:00:00 | 70                  | 20.82                   |
| 2024-01-15 11:00:00 | 40                  | 21.21                   |

## Related articles

* **Stages**: [`windowcomp`](../stages/windowcomp), [`comp`](../stages/comp), [`sort`](../stages/sort)
* **Functions**: [`stddev_sample (comp)`](stddev_sample_with_comp_stage), [`stddev_population()`](stddev_population_with_windowcomp_stage), [`avg()`](avg_with_windowcomp_stage)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
