# extract\_time

Use the `extract_time()` function to isolate and return specific components of a timestamp, such as the year, month, or hour.

Important Note: The values returned by `extract_time()` are always based on GMT (Greenwich Mean Time), even if your server settings for Timezone or Timestamp Format are adjusted.

## Syntax

```sql
extract_time (<timestamp>, <part>)
```

## Parameters

| Name        | Type      | Required | Description                                                                            |
| ----------- | --------- | -------- | -------------------------------------------------------------------------------------- |
| `timestamp` | timestamp | Yes      | The input timestamp value, originating from a field or the result of another function. |
| `part`      | string    | Yes      | The specific unit of the timestamp to extract.                                         |

## Returns

The `extract_time()` function returns a numerical value (Integer or Number) representing the extracted portion of the timestamp.

## Usage notes

* The values returned by `extract_time()` are always based on GMT (Greenwich Mean Time) even if you've adjusted the Timezone or Timestamp Format server settings. For more information on the server settings, see Configure server settings.
* The `part` parameter is not case-sensitive, but the string must match one of the supported keywords.
* The supported keywords for the `part` parameter are:
  * `DAY`: Day of the month (1-31).
  * `DAYOFWEEK`: Day of the week (1=Monday, 7=Sunday).
  * `DAYOFYEAR`: Day of the year (1-366).
  * `HOUR`: Hour of the day (0-23).
  * `MICROSECOND`: Microseconds.
  * `MILLISECOND`: Milliseconds.
  * `MINUTE`: Minute of the hour (0-59).
  * `MONTH`: Month of the year (1-12).
  * `QUARTER`: Quarter of the year (1-4).
  * `SECOND`: Second of the minute (0-59).
  * `YEAR`: Year (for example, 2023).

## Examples

### Example 1: Extracting the YEAR

**Goal**: Extract the year from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_year = extract_time(_time, "YEAR") 
| fields event_id, _time, event_year 
| limit 3 
```

**Explanation**: The `event_year` field shows the integer year (2023) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_YEAR |
| --------- | ---------------------- | ----------- |
| 101       | Oct 26th 2023 10:00:00 | 2023        |
| 102       | Oct 26th 2023 10:05:30 | 2023        |
| 103       | Oct 26th 2023 10:15:15 | 2023        |

### Example 2: Extracting the MONTH

**Goal**: Extract the month from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_month = extract_time(_time, "MONTH") 
| fields event_id, _time, event_month 
| limit 3 
```

**Explanation**: The `event_month` field shows the integer month (10 for October) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_MONTH |
| --------- | ---------------------- | ------------ |
| 101       | Oct 26th 2023 10:00:00 | 10           |
| 102       | Oct 26th 2023 10:05:30 | 10           |
| 103       | Oct 26th 2023 10:15:15 | 10           |

### Example 3: Extracting the DAY

**Goal**: Extract the day of the month from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_day = extract_time(_time, "DAY") 
| fields event_id, _time, event_day 
| limit 3 
```

**Explanation**: The `event_day` field shows the integer day of the month (26) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_DAY |
| --------- | ---------------------- | ---------- |
| 101       | Oct 26th 2023 10:00:00 | 26         |
| 102       | Oct 26th 2023 10:05:30 | 26         |
| 103       | Oct 26th 2023 10:15:15 | 26         |

### Example 4: Extracting the DAYOFWEEK

**Goal**: Extract the day of the week from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_day_of_week = extract_time(_time, "DAYOFWEEK") 
| fields event_id, _time, event_day_of_week 
| limit 3 
```

**Explanation**: The `event_day_of_week` field shows the integer day of the week (4 for Thursday) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_DAY\_OF\_WEEK |
| --------- | ---------------------- | -------------------- |
| 101       | Oct 26th 2023 10:00:00 | 4                    |
| 102       | Oct 26th 2023 10:05:30 | 4                    |
| 103       | Oct 26th 2023 10:15:15 | 4                    |

### Example 5: Extracting the DAYOFYEAR

**Goal**: Extract the day of the year from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_day_of_year = extract_time(_time, "DAYOFYEAR") 
| fields event_id, _time, event_day_of_year 
| limit 3 
```

**Explanation**: The `event_day_of_year` field shows the integer day of the year (299) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_DAY\_OF\_YEAR |
| --------- | ---------------------- | -------------------- |
| 101       | Oct 26th 2023 10:00:00 | 299                  |
| 102       | Oct 26th 2023 10:05:30 | 299                  |
| 103       | Oct 26th 2023 10:15:15 | 299                  |

### Example 6: Extracting the HOUR

**Goal**: Extract the hour from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_hour = extract_time(_time, "HOUR") 
| fields event_id, _time, event_hour 
| limit 3 
```

**Explanation**: The `event_hour` field shows the integer hour (10) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_HOUR |
| --------- | ---------------------- | ----------- |
| 101       | Oct 26th 2023 10:00:00 | 10          |
| 102       | Oct 26th 2023 10:05:30 | 10          |
| 103       | Oct 26th 2023 10:15:15 | 10          |

### Example 7: Extracting the MINUTE

**Goal**: Extract the minute from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_minute = extract_time(_time, "MINUTE") 
| fields event_id, _time, event_minute 
| limit 3 
```

**Explanation**: The `event_minute` field shows the integer minute extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_MINUTE |
| --------- | ---------------------- | ------------- |
| 101       | Oct 26th 2023 10:00:00 | 0             |
| 102       | Oct 26th 2023 10:05:30 | 5             |
| 103       | Oct 26th 2023 10:15:15 | 15            |

### Example 8: Extracting the SECOND

**Goal**: Extract the second from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_second = extract_time(_time, "SECOND") 
| fields event_id, _time, event_second 
| limit 3 
```

**Explanation**: The `event_second` field shows the integer second extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_SECOND |
| --------- | ---------------------- | ------------- |
| 101       | Oct 26th 2023 10:00:00 | 0             |
| 102       | Oct 26th 2023 10:05:30 | 30            |
| 103       | Oct 26th 2023 10:15:15 | 15            |

### Example 9: Extracting the MILLISECOND

**Goal**: Extract the milliseconds from a timestamp. Because the sample data does not explicitly display milliseconds, this example uses `current_time()` for demonstration.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter current_ts_val = current_time() // Conceptual: Jul 25th 2024 14:30:45.123 
| alter ms_part = extract_time(current_ts_val, "MILLISECOND") 
| fields event_id, current_ts_val, ms_part 
| limit 3 
```

**Explanation**: The `ms_part` field shows the millisecond component (123) extracted from the current time. This illustrates the function's capability with higher precision timestamps.

**Output**:

| EVENT\_ID | CURRENT\_TS\_VAL       | MS\_PART |
| --------- | ---------------------- | -------- |
| 101       | Jul 25th 2024 14:30:45 | 123      |
| 102       | Jul 25th 2024 14:30:45 | 123      |
| 103       | Jul 25th 2024 14:30:45 | 123      |

### Example 10: Extracting the MICROSECOND

**Goal**: Extract the microseconds from a timestamp. Because the sample data does not explicitly display microseconds, this example uses `current_time()` for demonstration.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter current_ts_val = current_time() // Conceptual: Jul 25th 2024 14:30:45.123456 
| alter us_part = extract_time(current_ts_val, "MICROSECOND") 
| fields event_id, current_ts_val, us_part 
| limit 3 
```

**Explanation**: The `us_part` field shows the microsecond component (123456) extracted from the current time, demonstrating the function's precision.

**Output**:

| EVENT\_ID | CURRENT\_TS\_VAL       | US\_PART |
| --------- | ---------------------- | -------- |
| 101       | Jul 25th 2024 14:30:45 | 123456   |
| 102       | Jul 25th 2024 14:30:45 | 123456   |
| 103       | Jul 25th 2024 14:30:45 | 123456   |

### Example 11: Extracting the QUARTER

**Goal**: Extract the quarter of the year from the `_time` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_quarter = extract_time(_time, "QUARTER") 
| fields event_id, _time, event_quarter 
| limit 3 
```

**Explanation**: The `event_quarter` field shows the integer quarter of the year (4) extracted from each event's `_time` timestamp.

**Output**:

| EVENT\_ID | \_TIME                 | EVENT\_QUARTER |
| --------- | ---------------------- | -------------- |
| 101       | Oct 26th 2023 10:00:00 | 4              |
| 102       | Oct 26th 2023 10:05:30 | 4              |
| 103       | Oct 26th 2023 10:15:15 | 4              |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`current_time`](current_time)
