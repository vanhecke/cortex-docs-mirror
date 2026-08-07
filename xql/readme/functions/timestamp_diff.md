# timestamp\_diff

Use the `timestamp_diff()` function to calculate the numerical difference between two timestamps in a specified unit.

## Syntax

```sql
timestamp_diff (<timestamp1>, <timestamp2>, <part>)
```

## Parameters

| Name         | Type      | Required | Description                                                                                                                              |
| ------------ | --------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `timestamp1` | timestamp | Yes      | The first timestamp object in the comparison.                                                                                            |
| `timestamp2` | timestamp | Yes      | The second timestamp object, which is subtracted from the first.                                                                         |
| `part`       | string    | Yes      | The unit in which the difference is expressed. Supported values are `DAY`, `HOUR`, `MINUTE`, `SECOND`, `MILLISECOND`, and `MICROSECOND`. |

## Returns

The `timestamp_diff()` function returns a numerical value (integer or float) representing the difference between the two timestamps in the specified unit.

## Usage notes

* The function calculates the difference by subtracting `timestamp2` from `timestamp1`.
* If `timestamp1` is chronologically greater (later) than `timestamp2`, the function returns a positive value.
* If `timestamp1` is chronologically less (earlier) than `timestamp2`, the function returns a negative value.
* If the calculated difference in the specified unit results in a fractional value between 0 and 1 (exclusive of 1, inclusive of 0), the function returns 0.
* Supported values for the `part` parameter include: `DAY`, `HOUR`, `MINUTE`, `SECOND`, `MILLISECOND`, and `MICROSECOND`.

## Examples

### Example 1: Difference in seconds between current\_time() and\_time

**Goal**: Calculate the difference in seconds between the current query execution time and the event's timestamp.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter current_ts = current_time()
| alter event_ts = _time
| alter diff_in_seconds = timestamp_diff(current_ts, event_ts, "SECOND")
| fields event_id, event_ts, current_ts, diff_in_seconds
| limit 3
```

**Explanation**: The query computes the number of full seconds that have passed between the event's `_time` and the `current_time()` of the query execution.

**Output**:

| EVENT\_ID | EVENT\_TS              | CURRENT\_TS            | DIFF\_IN\_SECONDS |
| --------- | ---------------------- | ---------------------- | ----------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 26th 2023 12:00:00 | 7200              |
| 102       | Oct 26th 2023 10:05:30 | Oct 26th 2023 12:00:00 | 6870              |
| 103       | Oct 26th 2023 10:15:15 | Oct 26th 2023 12:00:00 | 6285              |

### Example 2: Difference in minutes between \_time and a static timestamp

**Goal**: Calculate the difference in minutes between the event timestamp and a specific static timestamp, demonstrating truncation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_ts = _time
| alter static_past_ts = parse_timestamp("%Y-%m-%d %H:%M:%S", "2023-10-26 10:05:00")
| alter diff_in_minutes = timestamp_diff(event_ts, static_past_ts, "MINUTE")
| fields event_id, event_ts, static_past_ts, diff_in_minutes
| limit 3
```

**Explanation**: The query calculates the difference in minutes. Note that partial minutes (values between 0 and 1) are truncated to 0.

**Output**:

| EVENT\_ID | EVENT\_TS              | STATIC\_PAST\_TS       | DIFF\_IN\_MINUTES |
| --------- | ---------------------- | ---------------------- | ----------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 26th 2023 10:05:00 | -5                |
| 102       | Oct 26th 2023 10:05:30 | Oct 26th 2023 10:05:00 | 0                 |
| 103       | Oct 26th 2023 10:15:15 | Oct 26th 2023 10:05:00 | 10                |

### Example 3: Difference in hours, yielding a negative result

**Goal**: Calculate the difference in hours where the first timestamp is earlier than the second, resulting in a negative value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_ts = _time
| alter static_future_ts = parse_timestamp("%Y-%m-%d %H:%M:%S", "2023-10-27 10:00:00")
| alter diff_in_hours = timestamp_diff(event_ts, static_future_ts, "HOUR")
| fields event_id, event_ts, static_future_ts, diff_in_hours
| limit 3
```

**Explanation**: The query demonstrates that when `timestamp1` is earlier than `timestamp2`, the result is negative. Calculations are truncated to full hours.

**Output**:

| EVENT\_ID | EVENT\_TS              | STATIC\_FUTURE\_TS     | DIFF\_IN\_HOURS |
| --------- | ---------------------- | ---------------------- | --------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 27th 2023 10:00:00 | -24             |
| 102       | Oct 26th 2023 10:05:30 | Oct 27th 2023 10:00:00 | -23             |
| 103       | Oct 26th 2023 10:15:15 | Oct 27th 2023 10:00:00 | -23             |

### Example 4: Using timestamp\_diff() in a filter stage

**Goal**: Filter events based on a calculated time difference relative to the current time.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter current_ts = current_time()
| filter timestamp_diff(current_ts, _time, "HOUR") > 1
| fields event_id, _time
| limit 3
```

**Explanation**: This query filters for events that occurred more than 1 hour prior to the current execution time.

**Output**:

| EVENT\_ID | \_TIME                 |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 |
| 102       | Oct 26th 2023 10:05:30 |
| 103       | Oct 26th 2023 10:15:15 |

### Example 5: Difference in milliseconds between \_time and a closely past static timestamp

**Goal**: Calculate a fine-grained difference in milliseconds between two close timestamps.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_ts = _time
| alter static_slightly_past_ts = parse_timestamp("%F %R:%E3S", "2023-10-26 10:00:00.000")
| alter diff_in_milliseconds = timestamp_diff(event_ts, static_slightly_past_ts, "MILLISECOND")
| fields event_id, event_ts, static_slightly_past_ts, diff_in_milliseconds
| limit 3
```

**Explanation**: The query calculates the exact difference in milliseconds, useful for precise time measurements.

**Output**:

| EVENT\_ID | EVENT\_TS              | STATIC\_SLIGHTLY\_PAST\_TS | DIFF\_IN\_MILLISECONDS |
| --------- | ---------------------- | -------------------------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 26th 2023 10:00:00     | 0                      |
| 102       | Oct 26th 2023 10:05:30 | Oct 26th 2023 10:00:00     | 330000                 |
| 103       | Oct 26th 2023 10:15:15 | Oct 26th 2023 10:00:00     | 915000                 |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`current_time`](current_time), [`parse_timestamp`](parse_timestamp)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
