# time\_frame\_end

Use the `time_frame_end()` function to return the timestamp object that represents the end of the time frame configured for the overall XQL query.

## Syntax

```sql
time_frame_end()
```

## Parameters

| Name | Type | Required | Description                                                                                                                  |
| ---- | ---- | -------- | ---------------------------------------------------------------------------------------------------------------------------- |
| None | N/A  | No       | This function does not require any input parameters. The function inherits the time frame from the `config timeframe` stage. |

## Returns

The `time_frame_end()` function returns a `TIMESTAMP` object representing the end of the query's time range.

## Usage notes

* The function returns the timestamp object in the format `MMM dd YYYY HH:mm:ss` (for example, `Jun 8th 2022 15:20:06`).
* The value returned directly corresponds to the end of the time range set by the `config timeframe` stage of the query.
* You can configure the time frame using the `config timeframe` stage, where the range can be relative or exact.
* If the `config timeframe` is set to a relative time (for example, `last 24H` or `between "-1h" and "now"`), `time_frame_end()` returns the `current_time()` at the moment the query is executed.
* This function is useful when the query uses a custom time frame whose end time is in the past.

## Examples

### Example 1: With a relative timeframe (last N units)

**Goal**: Capture the end time of the query when using a relative timeframe (for example, last 2 hours).

**XQL code**:

```sql
config timeframe = 2h // Sets the query timeframe to the last 2 hours from execution
| dataset = sample_xql_raw
| alter query_end_time = time_frame_end() // Captures the end of the query timeframe
| fields event_id, query_end_time
| limit 3
```

**Explanation**: The `config timeframe = 2h` specifies that the query should run for the last two hours from the moment it is executed, and because this is a relative timeframe, `time_frame_end()` returns the `current_time` at the moment of query execution.

**Output**:

| EVENT\_ID | QUERY\_END\_TIME       |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 12:00:00 |
| 102       | Oct 26th 2023 12:00:00 |
| 103       | Oct 26th 2023 12:00:00 |

### Example 2: With a relative timeframe (between relative start and "now")

**Goal**: Capture the end time of the query when using a relative timeframe ending in "now".

**XQL code**:

```sql
config timeframe between "-1h" and "now" // Sets the timeframe from 1 hour ago until now
| dataset = sample_xql_raw
| alter query_end_time = time_frame_end() // Captures the end of the query timeframe
| fields event_id, query_end_time
| limit 3
```

**Explanation**: Similar to Example 1, the use of `"now"` in the `config timeframe` means that `time_frame_end()` returns the `current_time` at the point of query execution. The resulting `query_end_time` reflects this execution time.

**Output**:

| EVENT\_ID | QUERY\_END\_TIME       |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 12:00:00 |
| 102       | Oct 26th 2023 12:00:00 |
| 103       | Oct 26th 2023 12:00:00 |

### Example 3: With an exact timeframe

**Goal**: Capture the end time of the query when using a precise, static start and end time.

**XQL code**:

```sql
config timeframe between "2023-10-26 09:00:00 UTC" and "2023-10-26 11:00:00 UTC" // Defines an exact timeframe
| dataset = sample_xql_raw
| alter query_end_time = time_frame_end() // Captures the end of the query's timeframe
| fields event_id, query_end_time
| limit 3
```

**Explanation**: When an exact timeframe is configured, `time_frame_end()` directly returns the explicitly defined end timestamp from the `config timeframe`. In this case, it returns the timestamp for 11:00:00 UTC on October 26th, 2023.

**Output**:

| EVENT\_ID | QUERY\_END\_TIME       |
| --------- | ---------------------- |
| 101       | Oct 26th 2023 11:00:00 |
| 102       | Oct 26th 2023 11:00:00 |
| 103       | Oct 26th 2023 11:00:00 |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields)
* **Functions**: [`current_time`](current_time), [`timestamp_diff`](timestamp_diff)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
