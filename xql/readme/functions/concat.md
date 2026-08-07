# concat

Use the `concat()` function to join two or more strings into a single, cohesive string.

## Syntax

```sql
concat (<string1>, <string2>, ...)
```

## Parameters

| Name                      | Type   | Required | Description                                                                           |
| ------------------------- | ------ | -------- | ------------------------------------------------------------------------------------- |
| `string1`, `string2`, ... | string | Yes      | The string expressions whose values will be joined. Two or more strings are required. |

## Returns

The `concat()` function returns a single string.

## Usage notes

* The function strictly accepts string parameters.
* The `concat()` function will not perform any implicit conversion of other data types to strings.
* Explicit `to_string()` conversion is necessary for non-string values (such as integers, floats, or booleans) to ensure type compatibility.
* If any of the values passed to `concat()` are `NULL`, the function will return `NULL`.

## Examples

### Example 1: Concatenating two string literal values

**Goal**: Join two static string values into a new field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter static_message = concat("Investigation: ", "Started") 
| fields event_id, static_message 
| limit 3
```

**Explanation**: For each record, the `concat()` function combines the two literal strings "Investigation: " and "Started", resulting in the value "Investigation: Started" for all records.

**Output**:

| EVENT\_ID | STATIC\_MESSAGE          |
| --------- | ------------------------ |
| 101       | "Investigation: Started" |
| 102       | "Investigation: Started" |
| 103       | "Investigation: Started" |

### Example 2: Concatenating a string literal with a field value

**Goal**: Join a fixed string prefix with the value of an existing field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_label = concat("Event ID: ", to_string(event_id)) 
| fields event_id, event_label 
| limit 3
```

**Explanation**: The `to_string(event_id)` function converts the numeric `event_id` into its string representation. `concat()` then joins the literal string "Event ID: " with the string version of the `event_id`, creating a unique `event_label` for each record.

**Output**:

| EVENT\_ID | EVENT\_LABEL    |
| --------- | --------------- |
| 101       | "Event ID: 101" |
| 102       | "Event ID: 102" |
| 103       | "Event ID: 103" |

### Example 3: Concatenating multiple field values

**Goal**: Combine values from multiple existing fields into a single string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_summary = concat(event_description, " (Success: ", to_string(is_successful), ", Duration: ", to_string(duration_seconds), ")") 
| fields event_id, event_description, is_successful, duration_seconds, event_summary 
| limit 3
```

**Explanation**: The functions `to_string(is_successful)` and `to_string(duration_seconds)` convert the boolean and numeric fields into strings. `concat()` then combines `event_description`, literal strings like " (Success: ", and the converted string representations into `event_summary`.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | IS\_SUCCESSFUL | DURATION\_SECONDS | EVENT\_SUMMARY                                                   |
| --------- | -------------------------------- | -------------- | ----------------- | ---------------------------------------------------------------- |
| 101       | "User login successful"          | true           | 1.5               | "User login successful (Success: true, Duration: 1.5)"           |
| 102       | "File access attempt"            | false          | 0.8               | "File access attempt (Success: false, Duration: 0.8)"            |
| 103       | "Network connection established" | true           | 10.2              | "Network connection established (Success: true, Duration: 10.2)" |

### Example 4: Concatenating extracted JSON scalar values

**Goal**: Use `concat()` with values extracted from a JSON field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter status_code_value = coalesce(simple_json_data -> code, simple_json_data -> error_code) 
| alter full_status_message = concat("Status: ", status_code_value) 
| fields event_id, simple_json_data, status_code_value, full_status_message 
| limit 3
```

**Explanation**: The `coalesce` function attempts to get either `code` or `error_code` from `simple_json_data` as a string. `concat()` combines "Status: " with the extracted `status_code_value`. Because `concat()` returns `NULL` if any input is `NULL`, `full_status_message` is `NULL` for event 103 where neither key exists.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | STATUS\_CODE\_VALUE | FULL\_STATUS\_MESSAGE    |
| --------- | ------------------------------------------------- | ------------------- | ------------------------ |
| 101       | {"status": "ok", "code": 200}                     | "200"               | "Status: 200"            |
| 102       | {"status": "fail", "error": "access\_denied"}     | "access\_denied"    | "Status: access\_denied" |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL                | NULL                     |

## Example 5: Concatenating converted boot time values

**Goal**: Use `concat()` to prepend a string prefix to a converted timestamp field.

**XQL code**:

```sql
dataset = xdr_data 
| fields action_boot_time as abt 
| filter abt != null 
| alter abt_string = concat("str: ", to_string(abt)) 
| limit 1
```

**Explanation**: The query filters the `xdr_data` dataset to find the first record where `action_boot_time` is not `NULL`. Since `action_boot_time` is typically a numeric or timestamp type, the `to_string()` function is used to convert it before the `concat()` function joins it with the literal prefix `"str: "`.

**Output**:

| ABT        | ABT\_STRING       |
| ---------- | ----------------- |
| 1675238400 | "str: 1675238400" |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`coalesce`](coalesce), [`to_string`](to_string)
