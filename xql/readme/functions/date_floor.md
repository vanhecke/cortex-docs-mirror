# date\_floor

Use the `date_floor()` function to return a new timestamp that is rounded down to the nearest whole value of a specified time unit.

## Syntax

```sql
date_floor (<timestamp field>, "<time_unit>" [, "<time zone>"])
```

## Parameters

| Name              | Type      | Required | Description                                                                                                                                                                                                                  |
| ----------------- | --------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `timestamp field` | timestamp | Yes      | The input timestamp value, originating from a field or the result of another function.                                                                                                                                       |
| `time_unit`       | string    | Yes      | The unit to which the timestamp should be rounded down. Supported values are `y` (year), `mo` (month), `w` (week), `d` (day), or `h` (hour). This parameter is not case-sensitive.                                           |
| `time_zone`       | string    | No       | The time zone to apply for the calculation. This can be an hours offset (for example, `+08:00`) or a time zone name from the List of Supported Time Zones, (for example, `America/Chicago`). If omitted, the default is UTC. |

## Returns

The `date_floor()` function returns a `TIMESTAMP` value rounded down to the beginning of the specified time unit.

## Usage notes

* The function always rounds the timestamp **down** to the beginning of the specified time unit. For example, `date_floor("2023-10-26 10:30:00 UTC", "h")` results in `2023-10-26 10:00:00`.
* Supported time units (`y`, `mo`, `w`, `d`, `h`) are not case-sensitive.
* This function is typically used within `alter` or `filter` stages to perform data transformations for time-based aggregation or analysis.

## Examples

### Example 1: Rounding \_time to the nearest hour (default UTC)

**Goal**: Round the `_time` field to the beginning of the hour using the default UTC time zone.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter floored_hour = date_floor(_time, "h") 
| fields event_id, _time, floored_hour 
| limit 3 
```

**Explanation**: The query rounds the `_time` field down to the start of the hour. For events occurring at 10:05:30 or 10:15:15, the result is 10:00:00.

**Output**:

| event\_id | \_time                 | floored\_hour          |
| --------- | ---------------------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 26th 2023 10:00:00 |
| 102       | Oct 26th 2023 10:05:30 | Oct 26th 2023 10:00:00 |
| 103       | Oct 26th 2023 10:15:15 | Oct 26th 2023 10:00:00 |

### Example 2: Rounding \_time to the nearest day (default UTC)

**Goal**: Round the `_time` field to the beginning of the day using the default UTC time zone.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter floored_day = date_floor(_time, "d") 
| fields event_id, _time, floored_day 
| limit 3 
```

**Explanation**: All `_time` values are rounded down to the very beginning of the day (midnight UTC) on October 26th, 2023.

**Output**:

| event\_id | \_time                 | floored\_day           |
| --------- | ---------------------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 26th 2023 00:00:00 |
| 102       | Oct 26th 2023 10:05:30 | Oct 26th 2023 00:00:00 |
| 103       | Oct 26th 2023 10:15:15 | Oct 26th 2023 00:00:00 |

### Example 3: Rounding \_time to the nearest week (default UTC)

**Goal**: Round the `_time` field to the beginning of the week using the default UTC time zone.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter floored_week = date_floor(_time, "w") 
| fields event_id, _time, floored_week 
| limit 3 
```

**Explanation**: Because October 26th, 2023, falls within the week starting Sunday, October 22nd, 2023, all timestamps are rounded down to the beginning of that week (midnight UTC on October 22nd).

**Output**:

| event\_id | \_time                 | floored\_week          |
| --------- | ---------------------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 22nd 2023 00:00:00 |
| 102       | Oct 26th 2023 10:05:30 | Oct 22nd 2023 00:00:00 |
| 103       | Oct 26th 2023 10:15:15 | Oct 22nd 2023 00:00:00 |

### Example 4: Rounding \_time to the nearest month (default UTC)

**Goal**: Round the `_time` field to the beginning of the month using the default UTC time zone.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter floored_month = date_floor(_time, "mo") 
| fields event_id, _time, floored_month 
| limit 3 
```

**Explanation**: All `_time` values are rounded down to the very beginning of October 2023 (midnight UTC on October 1st).

**Output**:

| event\_id | \_time                 | floored\_month        |
| --------- | ---------------------- | --------------------- |
| 101       | Oct 26th 2023 10:00:00 | Oct 1st 2023 00:00:00 |
| 102       | Oct 26th 2023 10:05:30 | Oct 1st 2023 00:00:00 |
| 103       | Oct 26th 2023 10:15:15 | Oct 1st 2023 00:00:00 |

### Example 5: Rounding \_time to the nearest year (default UTC)

**Goal**: Round the `_time` field to the beginning of the year using the default UTC time zone.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter floored_year = date_floor(_time, "y") 
| fields event_id, _time, floored_year 
| limit 3 
```

**Explanation**: All `_time` values are rounded down to the very beginning of 2023 (midnight UTC on January 1st).

**Output**:

| event\_id | \_time                 | floored\_year         |
| --------- | ---------------------- | --------------------- |
| 101       | Oct 26th 2023 10:00:00 | Jan 1st 2023 00:00:00 |
| 102       | Oct 26th 2023 10:05:30 | Jan 1st 2023 00:00:00 |
| 103       | Oct 26th 2023 10:15:15 | Jan 1st 2023 00:00:00 |

### Example 6: Rounding current\_time() to the nearest day with a specific time zone

**Goal**: Round the current time (assumed here as Jul 25th 2024 14:30:00 UTC) to the start of the day in a specific time zone ("America/Los\_Angeles").

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter current_time_val = current_time() 
| alter floored_day_la = date_floor(current_time_val, "d", "America/Los_Angeles") 
| fields event_id, current_time_val, floored_day_la 
| limit 3 
```

**Explanation**: The function converts the UTC time to the Los Angeles time zone (PDT, UTC-7), rounds it to the start of that day (midnight PDT), and returns the timestamp. Midnight PDT translates to 07:00:00 UTC.

**Output**:

| event\_id | current\_time\_val     | floored\_day\_la       |
| --------- | ---------------------- | ---------------------- |
| 101       | Jul 25th 2024 14:30:00 | Jul 25th 2024 07:00:00 |
| 102       | Jul 25th 2024 14:30:00 | Jul 25th 2024 07:00:00 |
| 103       | Jul 25th 2024 14:30:00 | Jul 25th 2024 07:00:00 |

### Example 7: Filtering events relative to the start of the week with timezone adjustment

**Goal**: Return up to 100 records from the `xdr_data` dataset where the event time (`_time`) is earlier than a calculated timestamp. The calculation determines the start of the current week in the "America/Los\_Angeles" timezone and subtracts exactly 24 days (2,073,600 seconds) from that point.

**XQL Code**:

```sql
dataset = sample_xql_raw
| filter _time < to_timestamp(add(to_epoch(date_floor(current_time(),"w", "America/Los_Angeles")),-2073600))
| limit 100

```

**Explanation**: This query performs a multi-step time transformation to create a dynamic filter:

1. current\_time() retrieves the present time.
2. date\_floor(..., "w", "America/Los\_Angeles") rounds that time down to the beginning of the week based on Los Angeles time.
3. to\_epoch(...) converts that "start of week" timestamp into a Unix epoch integer (seconds).
4. add(..., -2073600) subtracts 2,073,600 seconds (equivalent to 24 days) from the epoch value.
5. to\_timestamp(...) converts the resulting integer back into a standard timestamp format.
6. The filter stage then compares the \_time of every record against this calculated value.

**Output**:

| \_time                  | event\_id | event\_type          |
| ----------------------- | --------- | -------------------- |
| 2023-10-01 14:20:00 UTC | 88412     | ENHANCED\_EVENT\_LOG |
| 2023-09-28 09:15:30 UTC | 88305     | STORYLINE            |
| 2023-09-25 22:10:00 UTC | 88112     | BROWSER\_QUERY       |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`current_time`](current_time)
