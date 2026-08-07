# to\_number

Use the `to_number()` function to convert a string value that represents a number or a numeric data type into a floating-point number.

## Syntax

```sql
to_number (<string>)
```

## Parameters

| Name     | Type   | Required | Description                                                             |
| -------- | ------ | -------- | ----------------------------------------------------------------------- |
| `string` | string | Yes      | The string field or literal value that you wish to convert to a number. |

## Returns

The `to_number()` function returns a floating-point number.

## Usage notes

* The function requires a string value that represents a number or a numeric data type.
* The function is functionally identical to the `to_float()` function.
* The function consistently returns a floating-point number. Even if the input string represents a whole integer (for example, "200"), the output will be a floating-point number (for example, 200.0).
* If the input string cannot be successfully converted to a numeric value (for example, it contains letters or unparseable characters), the function will return `NULL`.
* If the input string itself is `NULL`, the function will return `NULL`.

## Examples

### Example 1: Converting a literal integer string

**Goal**: Convert a string literal representing an integer into a numerical (float) value.

**XQL code**:

```sql
config timeframe = 1d // Sets the query time context 
| dataset = sample_xql_raw // Specifies the dataset to use 
| alter converted_integer_string = to_number("42") // Converts a literal string "42" to a number 
| fields event_id, converted_integer_string // Selects relevant fields for display 
| limit 3 // Limits the output for brevity 
```

**Explanation**: The literal string "42" is successfully converted by `to_number()` into a floating-point number `42.0`.

**Output**:

| EVENT\_ID | CONVERTED\_INTEGER\_STRING |
| --------- | -------------------------- |
| 101       | 42.0                       |
| 102       | 42.0                       |
| 103       | 42.0                       |

### Example 2: Converting a literal floating-point string

**Goal**: Convert a string literal representing a decimal number into a floating-point value.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_float_string = to_number("123.45") // Converts a literal string "123.45" to a number 
| fields event_id, converted_float_string 
| limit 3 
```

**Explanation**: The literal string "123.45" is correctly converted into the floating-point number `123.45`.

**Output**:

| EVENT\_ID | CONVERTED\_FLOAT\_STRING |
| --------- | ------------------------ |
| 101       | 123.45                   |
| 102       | 123.45                   |
| 103       | 123.45                   |

### Example 3: Converting a numeric string extracted from a JSON field

**Goal**: Extract a numerical value from a JSON string field and convert it from its string representation to a number.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_code_as_string = simple_json_data -> code // Extracts 'code' as a string 
| alter converted_json_code = to_number(extracted_code_as_string) // Converts the extracted string to a number 
| fields event_id, simple_json_data, converted_json_code 
| limit 3 
```

**Explanation**: For `event_id` 101, the "code" value "200" is extracted as a string and then successfully converted to the number `200.0`. For `event_id` 102 and 103, where `simple_json_data` does not contain a "code" field, `extracted_code_as_string` becomes `NULL`, and subsequently, `converted_json_code` also becomes `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | CONVERTED\_JSON\_CODE |
| --------- | ------------------------------------------------- | --------------------- |
| 101       | {"status": "ok", "code": 200}                     | 200.0                 |
| 102       | {"status": "fail", "error": "access\_denied"}     | NULL                  |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL                  |

### Example 4: Attempting to convert a string with non-numeric characters

**Goal**: Demonstrate the behavior when attempting to convert a string that contains non-numerical characters.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter mem_free_string = nested_json_data -> system.mem_free // Extracts "80%" as a string 
| alter converted_mem_free = to_number(mem_free_string) // Attempts to convert "80%" to a number 
| fields event_id, nested_json_data, converted_mem_free 
| filter event_id = 104 // Focus on the relevant record for this example 
| limit 1 
```

**Explanation**: `to_number()` cannot perform the conversion and returns `NULL` for invalid inputs because "80%" is not a pure numeric string.

**Output**:

| EVENT\_ID | NESTED\_JSON\_DATA                                                      | CONVERTED\_MEM\_FREE |
| --------- | ----------------------------------------------------------------------- | -------------------- |
| 104       | {"system": {"cpu\_util": 0.15, "mem\_free": "80%"}, "status": "active"} | NULL                 |

### Example 5: Converting a `NULL` input field

**Goal**: Demonstrate the behavior when the input field is explicitly `NULL`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 105 // Focus on the relevant record for this example
| alter null_input_field = dst_domain // This field is NULL for some records (for example, event_id 105) 
| alter converted_null = to_number(null_input_field) // Attempts to convert a NULL field to a number 
| fields event_id, dst_domain, converted_null 
| limit 1 
```

**Explanation**: When the input to `to_number()` is `NULL`, the function consistently returns `NULL`.

**Output**:

| EVENT\_ID | DST\_DOMAIN | CONVERTED\_NULL |
| --------- | ----------- | --------------- |
| 105       | NULL        | NULL            |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`to_float`](to_float), [`to_integer`](to_integer), [`json_extract_scalar`](json_extract_scalar)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
