# bin

Use the `bin` stage to discretize a continuous numerical field or timestamp into separate buckets, or "bins." This is commonly used to group data into ranges, like age groups or time intervals, for aggregation and analysis.

## Syntax

```sql
bin <field_name> span=<number><timescale>
```

## Parameters

| Name         | Type   | Required | Description                                                                                                                                                                                    |
| ------------ | ------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `field_name` | string | Yes      | The name of the numeric or timestamp field to be binned.                                                                                                                                       |
| `span`       | string | Yes      | The size of each bin. For timestamps, this is a number followed by a timescale suffix (for example, `1h`, `15m`, `1d`). For numeric fields, this is an integer representing the interval size. |

## Returns

The `bin` stage modifies the specified field in the dataset, replacing the original continuous values with the starting value of the bin interval they fall into. The resulting field retains its original name.

## Usage notes

* The `bin` stage is often used immediately before an aggregation stage like `comp` to group records by time or numeric ranges.
* Binning simplifies complex continuous data by separating it into manageable categories.
* When binning timestamps, the returned value is the start time of the interval. For example, with `span=1h`, a timestamp of `10:45` becomes `10:00`.
* The `span` parameter determines the granularity of the groups.

## Examples

### Example 1: Binning by time

**Goal**: Group events into 1-hour intervals to prepare for counting events per hour.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| bin _time span = 1h
| comp count(event_id) as events_per_hour by _time
| fields _time, events_per_hour
```

**Explanation**: The `_time` field is binned into 1-hour buckets. The `comp` stage then counts the number of events that fall into each hour, creating a timeline of activity.

**Output:**

| \_time              | events\_per\_hour |
| ------------------- | ----------------- |
| 2023-10-26 10:00:00 | 45                |
| 2023-10-26 11:00:00 | 32                |
| 2023-10-26 12:00:00 | 50                |

### Example 2: Binning numeric values

**Goal**: Group file sizes into buckets of 100MB to analyze the distribution of file sizes.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter file_size_mb = divide(file_size, 1024 * 1024)
| bin file_size_mb span = 100
| comp count(event_id) as file_count by file_size_mb
| fields file_size_mb, file_count
```

**Explanation**: First, file size is converted to megabytes. Then, `bin` groups these sizes into 100MB intervals (0-100, 100-200, etc.). The `comp` stage counts how many files fall into each size range.

**Output:**

| file\_size\_mb | file\_count |
| -------------- | ----------- |
| 0              | 150         |
| 100            | 40          |
| 200            | 12          |

## Related articles

* **Stages**: [`comp`](comp), [`alter`](alter)
* **Functions**: [`count`](../functions/count_with_windowcomp_stage), [`divide`](../functions/divide)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
