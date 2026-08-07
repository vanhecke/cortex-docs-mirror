# parse\_epoch

Use the `parse_epoch()` function to return a Unix epoch integer value by converting a string representation of a timestamp.

## Syntax

```sql
parse_epoch ("<format_string>", <timestamp field>)
parse_epoch ("<format_string>", <timestamp field>, "<time_zone>")
parse_epoch ("<format_string>", <timestamp field>, "<time_zone>", "<time_unit>")
```

## Parameters

| Name              | Type   | Required | Description                                                                                                                           |
| ----------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `format_string`   | string | Yes      | Defines the layout of the input timestamp string (for example, `%Y-%m-%d %H:%M:%S`).                                                  |
| `timestamp_field` | string | Yes      | The string containing the timestamp to be parsed.                                                                                     |
| `time_zone`       | string | No       | An optional time zone specified by hours offset (for example, `+08:00`) or name (for example, `America/Chicago`). The default is UTC. |
| `time_unit`       | string | No       | Specifies the granularity of the returned integer (SECONDS, MILLIS, MICROS). The default is SECONDS.                                  |

## Returns

The `parse_epoch()` function returns a Unix epoch integer value.

## Usage notes

* The order of `time_zone` and `time unit` is important.
* If you're using the `time_zone` argument, you must define it immediately before the `time_unit` argument.
* If you use `time_zone` after `time_unit`, the default time zone (UTC) is used, and the configured value is ignored.
* To display the returned integer as a human-readable timestamp, it is typically passed to the `to_timestamp()` function.

## Examples

### Example 1: Without a time zone or time unit configured (implicit UTC, seconds)

**Goal**: Convert a timestamp string into an epoch integer using the default UTC time zone and SECONDS unit, then display it as a timestamp.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter new_time = to_timestamp(parse_epoch("%Y-%m-%d %H:%M:%S", "2023-10-26 10:00:00")) 
| fields event_id, new_time 
| limit 3 
```

**Explanation**: The input string "2023-10-26 10:00:00" is parsed using the format "%Y-%m-%d %H:%M:%S". Because no time zone is specified, `parse_epoch()` interprets it as a UTC timestamp. `to_timestamp()` then converts the resulting epoch seconds back to a TIMESTAMP object for display.

**Output**:

| EVENT\_ID | NEW\_TIME              |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 10:00:00 |
| 102       | Oct 26th 2023 10:00:00 |
| 103       | Oct 26th 2023 10:00:00 |

### Example 2: With a time zone configured using an hours offset

**Goal**: Convert a timestamp string interpreting it relative to a +03:00 hours offset.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter new_time = to_timestamp(parse_epoch("%Y-%m-%d %H:%M:%S", "2023-10-26 10:00:00", "+03:00")) 
| fields event_id, new_time 
| limit 3 
```

**Explanation**: The input string 10:00:00 is interpreted as being in a +03:00 time zone. When converted to UTC (which epoch time is based on), it becomes 07:00:00 UTC. This UTC time is then returned as the TIMESTAMP object.

**Output**:

| EVENT\_ID | NEW\_TIME              |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 07:00:00 |
| 102       | Oct 26th 2023 07:00:00 |
| 103       | Oct 26th 2023 07:00:00 |

### Example 3: With a time zone name configured

**Goal**: Convert a timestamp string interpreting it relative to the "America/Chicago" time zone.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter new_time = to_timestamp(parse_epoch("%Y-%m-%d %H:%M:%S", "2023-10-26 10:00:00", "America/Chicago")) 
| fields event_id, new_time 
| limit 3 
```

**Explanation**: The input string 10:00:00 is interpreted as being in the "America/Chicago" time zone (UTC-5 for this date). To convert to UTC, 5 hours are added, resulting in 15:00:00 UTC.

**Output**:

| EVENT\_ID | NEW\_TIME              |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 15:00:00 |
| 102       | Oct 26th 2023 15:00:00 |
| 103       | Oct 26th 2023 15:00:00 |

### Example 4: With both time zone and time unit configured

**Goal**: Convert a timestamp string using a +03:00 hours offset and explicitly return the epoch in MILLIS (milliseconds).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter new_time = to_timestamp(parse_epoch("%Y-%m-%d %H:%M:%S", "2023-10-26 10:00:00", "+03:00", "MILLIS"), "MILLIS") 
| fields event_id, new_time 
| limit 3 
```

**Explanation**: The input string is interpreted within the +03:00 time zone (converting 10:00:00 to 07:00:00 UTC). `parse_epoch()` generates the epoch value in milliseconds. This integer is then converted to a TIMESTAMP object using `to_timestamp()` with the "MILLIS" unit.

**Output**:

| EVENT\_ID | NEW\_TIME              |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 07:00:00 |
| 102       | Oct 26th 2023 07:00:00 |
| 103       | Oct 26th 2023 07:00:00 |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`to_timestamp`](to_timestamp)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
