# to\_float

Use the `to_float()` function to convert a string value that represents a number or a numeric data type into a floating-point number.

## Syntax

```sql
to_float (<string>)
```

## Parameters

| Name     | Type   | Required | Description                                                             |
| -------- | ------ | -------- | ----------------------------------------------------------------------- |
| `string` | string | Yes      | The string field or literal value that you wish to convert to a number. |

## Returns

The `to_float()` function returns a floating-point number.

## Usage notes

* The function is functionally identical to the `to_number()` function.
* The function consistently returns a floating-point number. Even if the input string represents a whole integer (for example, "200"), the output will be a floating-point number (for example, 200.0).
* If the input string does not represent a valid number (for example, contains letters or unparseable characters), or if the input itself is `NULL`, the function will return `NULL`.

## Examples

### Example 1: Converting a literal string (decimal representation) to float

**Goal**: Convert a string literal that represents a decimal number directly into a floating-point number.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter float_from_decimal_string = to_float("1.5") 
| fields event_id, float_from_decimal_string 
| limit 3
```

**Explanation**: The literal string "1.5" is converted to a float.

**Output**:

| EVENT\_ID | FLOAT\_FROM\_DECIMAL\_STRING |
| --------- | ---------------------------- |
| 101       | 1.5                          |
| 102       | 1.5                          |
| 103       | 1.5                          |

### Example 2: Converting a literal string (integer representation) to float

**Goal**: Convert a string literal that represents a whole number into its floating-point equivalent.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter float_from_integer_string = to_float("100") 
| fields event_id, float_from_integer_string 
| limit 3
```

**Explanation**: The literal string "100" is converted to the floating-point number 100.0.

**Output**:

| EVENT\_ID | FLOAT\_FROM\_INTEGER\_STRING |
| --------- | ---------------------------- |
| 101       | 100.0                        |
| 102       | 100.0                        |
| 103       | 100.0                        |

### Example 3: Converting a string extracted from JSON to float

**Goal**: Extract a numeric value (`code`) from a JSON string field (`simple_json_data`) and convert that extracted string to a float.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter json_code_string = simple_json_data -> code 
| alter converted_json_code = to_float(json_code_string) 
| fields event_id, simple_json_data, json_code_string, converted_json_code 
| limit 3
```

**Explanation**: For `event_id` 101, the "code" value "200" is extracted as a string and converted to the number 200.0. For events where the field is missing, it returns NULL.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | JSON\_CODE\_STRING | CONVERTED\_JSON\_CODE |
| --------- | ------------------------------------------------- | ------------------ | --------------------- |
| 101       | {"status": "ok", "code": 200}                     | "200"              | 200.0                 |
| 102       | {"status": "fail", "error": "access\_denied"}     | NULL               | NULL                  |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL               | NULL                  |

### Example 4: Converting an integer field (via `to_string()`) to float

**Goal**: Convert an existing integer field (`event_id`) to a string first using `to_string()`, and then convert that string representation into a float.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_id_as_string = to_string(event_id) 
| alter float_event_id = to_float(event_id_as_string) 
| fields event_id, event_id_as_string, float_event_id 
| limit 3
```

**Explanation**: The numeric `event_id` (for example, 101) is converted to a string "101", and then back to a float 101.0.

**Output**:

| EVENT\_ID | EVENT\_ID\_AS\_STRING | FLOAT\_EVENT\_ID |
| --------- | --------------------- | ---------------- |
| 101       | "101"                 | 101.0            |
| 102       | "102"                 | 102.0            |
| 103       | "103"                 | 103.0            |

### Example 5: Handling non-numeric string input (returns `NULL`)

**Goal**: Demonstrate the function's behavior when provided with a string that cannot be interpreted as a number (for example, a purely textual field like `event_description`).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter non_numeric_string = event_description 
| alter float_conversion_result = to_float(non_numeric_string) 
| fields event_id, non_numeric_string, float_conversion_result 
| limit 3
```

**Explanation**: Since `event_description` contains text (for example, "User login successful"), `to_float()` returns NULL.

**Output**:

| EVENT\_ID | NON\_NUMERIC\_STRING             | FLOAT\_CONVERSION\_RESULT |
| --------- | -------------------------------- | ------------------------- |
| 101       | "User login successful"          | NULL                      |
| 102       | "File access attempt"            | NULL                      |
| 103       | "Network connection established" | NULL                      |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`filter`](../stages/filter)
* **Functions**: [`to_number`](to_number), [`to_integer`](to_integer), [`to_string`](to_string)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
