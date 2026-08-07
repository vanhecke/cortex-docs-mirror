# to\_json\_string

Use the `to_json_string()` function to convert values of any data type into a JSON formatted string.

## Syntax

```sql
to_json_string(<data type>)
```

## Parameters

| Name        | Type                                    | Required | Description                            |
| ----------- | --------------------------------------- | -------- | -------------------------------------- |
| `data type` | integer, boolean, string, object, array | Yes      | The field or literal value to convert. |

## Returns

The `to_json_string()` function returns a string.

## Usage notes

* The function is versatile and accepts all data types, including integers, booleans, strings, objects, and arrays.
* When the input is an object or an array, the function returns a JSON formatted string representation of that input, preserving its structure.
* When the input is a simple string, it returns the string as its JSON literal representation (in other words, enclosed in quotes, with any internal special characters properly escaped if necessary).
* For numeric or boolean inputs, it converts them into their JSON string literal representations (for example, a number `101` becomes the string `"101"`, a boolean `true` becomes the string `"true"`).
* This function is particularly useful for standardizing data types for consistent processing or preparing complex data types for functions that require JSON string inputs, such as `json_extract()`.

## Examples

### Example 1: Converting a string field

**Goal**: Convert the `event_description` string field into its JSON string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter description_as_json = to_json_string(event_description)
| fields event_id, event_description, description_as_json
| limit 3
```

**Explanation**: The `to_json_string()` function takes the `event_description` string and returns it formatted as a JSON string literal.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | DESCRIPTION\_AS\_JSON            |
| --------- | -------------------------------- | -------------------------------- |
| 101       | "User login successful"          | "User login successful"          |
| 102       | "File access attempt"            | "File access attempt"            |
| 103       | "Network connection established" | "Network connection established" |

### Example 2: Converting a numeric field (integer)

**Goal**: Convert the `event_id` integer field into its JSON string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_as_json = to_json_string(event_id)
| fields event_id, event_id_as_json
| limit 3
```

**Explanation**: The integer `event_id` is converted into a string format suitable for JSON.

**Output**:

| EVENT\_ID | EVENT\_ID\_AS\_JSON |
| --------- | ------------------- |
| 101       | "101"               |
| 102       | "102"               |
| 103       | "103"               |

### Example 3: Converting a numeric field (float)

**Goal**: Convert the `duration_seconds` floating-point number field into its JSON string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter duration_as_json = to_json_string(duration_seconds)
| fields event_id, duration_seconds, duration_as_json
| limit 3
```

**Explanation**: The floating-point `duration_seconds` field is converted into a string format.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | DURATION\_AS\_JSON |
| --------- | ----------------- | ------------------ |
| 101       | 1.5               | "1.5"              |
| 102       | 0.8               | "0.8"              |
| 103       | 10.2              | "10.2"             |

### Example 4: Converting a boolean field

**Goal**: Convert the `is_successful` boolean field into its JSON string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter successful_as_json = to_json_string(is_successful)
| fields event_id, is_successful, successful_as_json
| limit 3
```

**Explanation**: The boolean `is_successful` values (`true` or `false`) are converted into their corresponding string representations.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | SUCCESSFUL\_AS\_JSON |
| --------- | -------------- | -------------------- |
| 101       | true           | "true"               |
| 102       | false          | "false"              |
| 103       | true           | "true"               |

### Example 5: Converting a JSON object field to a JSON string

**Goal**: Convert the `simple_json_data` field, which holds a JSON object, into a single JSON string.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter simple_data_as_json = to_json_string(simple_json_data)
| fields event_id, simple_json_data, simple_data_as_json
| limit 3
```

**Explanation**: The entire JSON object in `simple_json_data` is converted into a string. Note that the entire structure is enclosed in outer double quotes, and original double quotes within the JSON are escaped with a backslash (`\"`) to ensure it is a valid JSON string literal.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | SIMPLE\_DATA\_AS\_JSON                              |
| --------- | ------------------------------------------------- | --------------------------------------------------- |
| 101       | {"status": "ok", "code": 200}                     | "{"status": "ok", "code": 200}"                     |
| 102       | {"status": "fail", "error": "access\_denied"}     | "{"status": "fail", "error": "access\_denied"}"     |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | "{"connection\_id": "CONN-001", "protocol": "TCP"}" |

### Example 6: Converting an array of JSON objects field to a JSON string

**Goal**: Convert the `array_of_json_objects` field, which contains an array, into a JSON string.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter array_data_as_json = to_json_string(array_of_json_objects)
| fields event_id, array_of_json_objects, array_data_as_json
| limit 3
```

**Explanation**: The array structure, including its nested JSON objects, is converted into a single, correctly quoted and escaped string.

**Output**:

| EVENT\_ID | ARRAY\_OF\_JSON\_OBJECTS                                                              | ARRAY\_DATA\_AS\_JSON                                                                   |
| --------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| 101       | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}]  | "\[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}]"  |
| 102       | \[{"event": "file\_open", "path": "/etc/passwd"}]                                     | "\[{"event": "file\_open", "path": "/etc/passwd"}]"                                     |
| 103       | \[{"conn\_type": "outbound", "bytes": 1024}, {"conn\_type": "inbound", "bytes": 512}] | "\[{"conn\_type": "outbound", "bytes": 1024}, {"conn\_type": "inbound", "bytes": 512}]" |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`json_extract`](json_extract), [`json_extract_array`](json_extract_array), [`json_extract_scalar`](json_extract_scalar)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
