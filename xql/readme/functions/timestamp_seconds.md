# timestamp\_seconds

Use the `timestamp_seconds()` function to convert an integer value representing Unix epoch time in seconds into a timestamp.

## Syntax

```sql
timestamp_seconds (<integer>)
```

## Parameters

| Name      | Type    | Required | Description                                                                                                             |
| --------- | ------- | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| `integer` | integer | Yes      | The numerical value representing epoch time in seconds. This can be a literal integer or a field containing an integer. |

## Returns

The `timestamp_seconds()` function returns a timestamp compatible value, typically formatted as `MMM dd YYYY HH:mm:ss`.

## Usage notes

* The function expects a single integer input, which is implicitly interpreted as the number of seconds that have passed since the Unix epoch (January 1, 1970, 00:00:00 UTC).
* Endpoint Detection and Response (EDR) columns often store epoch values in milliseconds. Ensure your input is in seconds; otherwise, consider using `to_timestamp()` with the appropriate unit specification.
* If the input integer field or literal is `NULL`, the function returns `NULL`.
* If the integer input value is not a sensible epoch time (for example, an extremely large or small non-epoch value), the function may return `NULL` or an unexpected timestamp.

## Examples

### Example 1: Converting a literal epoch second integer

**Goal**: Convert a static integer literal (representing a known epoch second value) into a human-readable timestamp.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter known_epoch_seconds = 1698304800
| alter converted_timestamp = timestamp_seconds(known_epoch_seconds)
| fields event_id, known_epoch_seconds, converted_timestamp
| limit 3
```

**Explanation**: The query takes the `known_epoch_seconds` integer (which is 1698304800, representing 2023-10-26 10:00:00 UTC) and converts it to its corresponding timestamp value.

**Output**:

| EVENT\_ID | KNOWN\_EPOCH\_SECONDS | CONVERTED\_TIMESTAMP   |
| --------- | --------------------- | ---------------------- |
| 101       | 1698304800            | Oct 26th 2023 10:00:00 |
| 102       | 1698304800            | Oct 26th 2023 10:00:00 |
| 103       | 1698304800            | Oct 26th 2023 10:00:00 |

### Example 2: Converting an integer field to a timestamp

**Goal**: Apply the function to an existing integer field to interpret it as an epoch timestamp.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_as_timestamp = timestamp_seconds(to_integer(event_id))
| fields event_id, event_id_as_timestamp
| limit 3
```

**Explanation**: The integer value of `event_id` is interpreted as the number of seconds past the Unix epoch. For example, 101 becomes 101 seconds past epoch.

**Output**:

| EVENT\_ID | EVENT\_ID\_AS\_TIMESTAMP |
| --------- | ------------------------ |
| 101       | Jan 1st 1970 00:01:41    |
| 102       | Jan 1st 1970 00:01:42    |
| 103       | Jan 1st 1970 00:01:43    |

### Example 3: Converting a derived integer from a JSON field to a timestamp

**Goal**: Extract a numerical value from a JSON field, convert it to an integer, and then convert that integer to a timestamp.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter status_code_string = simple_json_data -> code
| alter status_code_int = to_integer(status_code_string)
| alter status_code_timestamp = timestamp_seconds(status_code_int)
| fields event_id, simple_json_data, status_code_string, status_code_int, status_code_timestamp
| limit 3
```

**Explanation**: For event 101, the code value `200` is extracted, converted to an integer, and interpreted as 200 seconds from epoch. For events where the field is missing, the result is `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | STATUS\_CODE\_STRING | STATUS\_CODE\_INT | STATUS\_CODE\_TIMESTAMP |
| --------- | ------------------------------------------------- | -------------------- | ----------------- | ----------------------- |
| 101       | {"status": "ok", "code": 200}                     | "200"                | 200               | Jan 1st 1970 00:03:20   |
| 102       | {"status": "fail", "error": "access\_denied"}     | NULL                 | NULL              | NULL                    |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL                 | NULL              | NULL                    |

### Example 4: Handling `NULL` input

**Goal**: Demonstrate the behavior when the function is provided with a `NULL` input.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter null_input_value = NULL
| alter converted_null_timestamp = timestamp_seconds(null_input_value)
| fields event_id, null_input_value, converted_null_timestamp
| limit 3
```

**Explanation**: The function returns `NULL` because the input is explicitly `NULL`.

**Output**:

| EVENT\_ID | NULL\_INPUT\_VALUE | CONVERTED\_NULL\_TIMESTAMP |
| --------- | ------------------ | -------------------------- |
| 101       | NULL               | NULL                       |
| 102       | NULL               | NULL                       |
| 103       | NULL               | NULL                       |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`to_integer`](to_integer)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
