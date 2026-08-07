# to\_epoch

Use the `to_epoch()` function to convert a timestamp value into the Unix epoch timestamp format.

## Syntax

```sql
to_epoch (<timestamp>, <time unit>)
```

## Parameters

| Name        | Type      | Required | Description                                                                                           |
| ----------- | --------- | -------- | ----------------------------------------------------------------------------------------------------- |
| `timestamp` | timestamp | Yes      | The timestamp value to convert. This must be a `TIMESTAMP` object, not a string.                      |
| `time unit` | string    | Yes      | The granularity of the returned integer value. Supported values are `SECONDS`, `MILLIS`, or `MICROS`. |

## Returns

The `to_epoch()` function returns an integer representing the Unix epoch timestamp.

## Usage notes

* The first parameter must be a `TIMESTAMP` object. If you have a string representation of a timestamp, you must first convert it to a `TIMESTAMP` object using functions like `parse_epoch()` or `to_timestamp()`.
* The `<time unit>` parameter specifies the granularity of the returned integer value (seconds, milliseconds, or microseconds).
* If no `<time unit>` is configured, `SECONDS` is used as the default.

## Examples

### Example 1: Converting \_time (timestamp field) to epoch in seconds

**Goal**: Convert the `_time` field, which is already a TIMESTAMP object, to its Unix epoch representation in seconds.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter epoch_seconds = to_epoch(_time, "SECONDS")
| fields event_id, _time, epoch_seconds
| limit 3
```

**Explanation**: The `_time` field is converted to an epoch integer in seconds using the "SECONDS" unit.

**Output**:

| EVENT\_ID | \_TIME                  | EPOCH\_SECONDS |
| --------- | ----------------------- | -------------- |
| 101       | 2023-10-26 10:00:00 UTC | 1698304800     |
| 102       | 2023-10-26 10:05:30 UTC | 1698305130     |
| 103       | 2023-10-26 10:15:15 UTC | 1698305715     |

### Example 2: Converting \_time (timestamp field) to epoch in milliseconds

**Goal**: Convert the `_time` field to its Unix epoch representation in milliseconds.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter epoch_millis = to_epoch(_time, "MILLIS")
| fields event_id, _time, epoch_millis
| limit 3
```

**Explanation**: The `_time` field is converted to an epoch integer in milliseconds using the "MILLIS" unit.

**Output**:

| EVENT\_ID | \_TIME                  | EPOCH\_MILLIS |
| --------- | ----------------------- | ------------- |
| 101       | 2023-10-26 10:00:00 UTC | 1698304800000 |
| 102       | 2023-10-26 10:05:30 UTC | 1698305130000 |
| 103       | 2023-10-26 10:15:15 UTC | 1698305715000 |

### Example 3: Converting \_time (timestamp field) to epoch in microseconds

**Goal**: Convert the `_time` field to its Unix epoch representation in microseconds.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter epoch_micros = to_epoch(_time, "MICROS")
| fields event_id, _time, epoch_micros
| limit 3
```

**Explanation**: The `_time` field is converted to an epoch integer in microseconds using the "MICROS" unit.

**Output**:

| EVENT\_ID | \_TIME                  | EPOCH\_MICROS    |
| --------- | ----------------------- | ---------------- |
| 101       | 2023-10-26 10:00:00 UTC | 1698304800000000 |
| 102       | 2023-10-26 10:05:30 UTC | 1698305130000000 |
| 103       | 2023-10-26 10:15:15 UTC | 1698305715000000 |

### Example 4: Converting a string timestamp to epoch

**Goal**: Convert a string that represents a timestamp into epoch time by first creating a TIMESTAMP object.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter literal_timestamp_string = "2023-10-26 10:00:00 UTC"
| alter parsed_timestamp_obj = parse_timestamp("%Y-%m-%d %H:%M:%S UTC", literal_timestamp_string)
| alter epoch_from_string = to_epoch(parsed_timestamp_obj, "SECONDS")
| fields event_id, literal_timestamp_string, parsed_timestamp_obj, epoch_from_string
| limit 3
```

**Explanation**: The query first uses `parse_timestamp()` to create a TIMESTAMP object from a string literal. Then, `to_epoch()` converts that object into epoch seconds.

**Output**:

| EVENT\_ID | LITERAL\_TIMESTAMP\_STRING | PARSED\_TIMESTAMP\_OBJ  | EPOCH\_FROM\_STRING |
| --------- | -------------------------- | ----------------------- | ------------------- |
| 101       | "2023-10-26 10:00:00 UTC"  | 2023-10-26 10:00:00 UTC | 1698304800          |
| 102       | "2023-10-26 10:00:00 UTC"  | 2023-10-26 10:00:00 UTC | 1698304800          |
| 103       | "2023-10-26 10:00:00 UTC"  | 2023-10-26 10:00:00 UTC | 1698304800          |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`parse_epoch`](parse_epoch), [`to_timestamp`](to_timestamp)
