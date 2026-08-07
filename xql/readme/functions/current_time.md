# current\_time

Use the `current_time()` function to return a `TIMESTAMP` value representing the exact time at which the query is executed.

## Syntax

```sql
current_time()
```

## Parameters

The `current_time()` function does not accept any parameters.

## Returns

The `current_time()` function returns a `TIMESTAMP` representing the current system time.

## Usage notes

* The functıon is particularly useful for calculations that require the current moment as a reference point, such as determining the age of an event or establishing dynamic time windows.
* The function returns the timestamp according to the default Timestamp Format specified in Server Settings.
* The function is typically used within the `alter` or `filter` stages.

## Examples

### Example 1: Assigning current\_time() to a new field in an alter stage

**Goal**: Create a new field that holds the current timestamp for each record.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter current_query_timestamp = current_time() 
| fields event_id, current_query_timestamp 
| limit 3
```

**Explanation**: The `current_time()` function provides the exact time of query execution, which is then assigned to the `current_query_timestamp` field for every record.

**Output**:

| EVENT\_ID | CURRENT\_QUERY\_TIMESTAMP |
| --------- | ------------------------- |
| 101       | Jul 25th 2024 14:30:00    |
| 102       | Jul 25th 2024 14:30:00    |
| 103       | Jul 25th 2024 14:30:00    |

### Example 2: Using current\_time() within timestamp\_diff() in a filter stage

**Goal**: Filter events that occurred more than 1 day ago relative to the current time.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter timestamp_diff(current_time(), _time, "DAY") > 1 
| fields event_id, _time 
| limit 3
```

**Explanation**: The `timestamp_diff()` function calculates the difference between the current time and the event's `_time`. The `filter` stage retains only those records where the difference is greater than 1 day.

**Output**:

| EVENT\_ID | \_TIME                 |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 |
| 102       | Oct 26th 2023 10:05:30 |
| 103       | Oct 26th 2023 10:15:15 |

### Example 3: Using current\_time() within date\_floor() in an alter Stage

**Goal**: Round the current time down to the nearest week.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter current_week_start = date_floor(current_time(), "w") 
| fields event_id, current_week_start 
| limit 3
```

**Explanation**: The `date_floor()` function, when applied to `current_time()`, truncates the timestamp to the beginning of the specified unit ("w" for week).

**Output**:

| EVENT\_ID | CURRENT\_WEEK\_START   |
| --------- | ---------------------- |
| 101       | Jul 21st 2024 00:00:00 |
| 102       | Jul 21st 2024 00:00:00 |
| 103       | Jul 21st 2024 00:00:00 |

### Example 4: Using current\_time() within extract\_time() in an alter Stage

**Goal**: Extract a specific part of the current time, such as the hour.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter current_hour = extract_time(current_time(), "HOUR") 
| fields event_id, current_hour 
| limit 3
```

**Explanation**: The `extract_time()` function isolates the "HOUR" component from the current timestamp provided by `current_time()`, returning an integer representing that hour.

**Output**:

| EVENT\_ID | CURRENT\_HOUR |
| --------- | ------------- |
| 101       | 14            |
| 102       | 14            |
| 103       | 14            |

### Example 5: Filtering events based on process execution age

**Goal**: From the `xdr_data` dataset, retrieve events from the last 24 hours where the actor process began running more than 30 days prior to the current time.

**XQL Code**:

```sql
dataset = sample_xql_raw
| filter timestamp_diff(current_time(), to_timestamp(actor_process_execution_time, "MILLIS"), "DAY") > 30
```

**Explanation**: This query uses current\_time() to get the present timestamp and to\_timestamp() to convert the actor\_process\_execution\_time (stored in milliseconds) into a standard timestamp format. The timestamp\_diff() function then calculates the number of days between these two points. The filter stage ensures only records with a difference greater than 30 days are returned.

**Output**

| event\_id | actor\_process\_execution\_time | \_time                  | calculated\_days\_old |
| --------- | ------------------------------- | ----------------------- | --------------------- |
| 5521      | 1693569600000                   | 2023-10-15 08:30:00 UTC | 44                    |
| 5589      | 1691064000000                   | 2023-10-15 09:12:00 UTC | 73                    |
| 5602      | 1688212800000                   | 2023-10-15 10:05:00 UTC | 106                   |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`timestamp_diff`](timestamp_diff), [`date_floor`](date_floor), [`extract_time`](extract_time)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
