# json\_extract

Use the `json_extract()` function to extract a specific JSON object or array from within a larger JSON-formatted string by navigating a specified path.

## Syntax

```sql
json_extract (<json_object_formatted_string>, <json_path>)
```

## Syntactic Sugar Format

```sql
<json_object_formatted_string> -> <json_path>{}
```

## Parameters

| Name                           | Type   | Required | Description                                                                                                                                                                                       |
| ------------------------------ | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `json_object_formatted_string` | string | Yes      | The field containing the JSON string from which to extract data. If the field is an object or array, use `to_json_string()` to convert it first.                                                  |
| `json_path`                    | string | Yes      | The path to the data within the JSON object. In regular syntax, it starts with `$`. In syntactic sugar, the `$` is omitted. Use brackets `['key']` or `["key"]` for keys with special characters. |

## Returns

The `json_extract()` function returns a string representation of the extracted JSON object or array.

## Usage notes

* **Input requirement**: The function requires a field that contains a JSON-formatted string. If your field is a native XQL object or array, you must convert it using `to_json_string()` before extraction.
* **Output format**: The function always returns a string. If the path points to a scalar value (string, number, boolean), it returns that value quoted as a JSON literal string. For direct scalar extraction without quotes (for numbers/booleans), consider using `json_extract_scalar()`.
* **Case sensitivity**: JSON field names are case-sensitive. The key in your `json_path` must exactly match the case of the field name in the JSON object.
* **Handling special characters**: When a field name in the path contains special characters like a dot (`.`) or colon (`:`):
  * **Regular syntax**: Use the syntax `json_extract(<json_object_formatted_string>, "['<json_field>']")`.
  * **Syntactic sugar syntax**: Use the syntax `<json_object_formatted_string> -> ["<json_field>"]{}`.
* **Error handling**: If the input string is not a valid JSON object, or if the specified `json_path` does not exist, the function returns `NULL`.

## Examples

### Example 1: Basic object property extraction

**Goal**: Extract a nested JSON object from a parent object.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_user_info = json_extract(to_json_string(nested_json_data), "$.user") 
| fields event_id, nested_json_data, extracted_user_info 
| limit 1
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_user_info = to_json_string(nested_json_data) -> user{} 
| fields event_id, nested_json_data, extracted_user_info 
| limit 1
```

**Explanation**: For `event_id` 101, the `nested_json_data` field contains a `user` object. The query converts the field to a JSON string and extracts the entire nested object, including keys and values.

**Output**:

| EVENT\_ID | NESTED\_JSON\_DATA                                         | EXTRACTED\_USER\_INFO         |
| --------- | ---------------------------------------------------------- | ----------------------------- |
| 101       | {"user": {"id": "U1", "name": "Alice"}, "session": {...\}} | {"id": "U1", "name": "Alice"} |

### Example 2: Extracting a deeper nested object property

**Goal**: Navigate deeper into a JSON structure to extract a specific nested object.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_session_info = json_extract(to_json_string(nested_json_data), "$.session") 
| fields event_id, nested_json_data, extracted_session_info 
| limit 1
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_session_info = to_json_string(nested_json_data) -> session{} 
| fields event_id, nested_json_data, extracted_session_info 
| limit 1
```

**Explanation**: The query extracts the `session` object, which is nested within `nested_json_data`, holding the session details.

**Output**:

| EVENT\_ID | NESTED\_JSON\_DATA                                             | EXTRACTED\_SESSION\_INFO          |
| --------- | -------------------------------------------------------------- | --------------------------------- |
| 101       | {"user": {...}, "session": {"start": "10:00", "type": "web"\}} | {"start": "10:00", "type": "web"} |

### Example 3: Extracting a JSON object from an array using index

**Goal**: Extract a specific JSON object from an array field using its index.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_first_action_obj = json_extract(to_json_string(array_of_json_objects), "$[0]") 
| fields event_id, array_of_json_objects, extracted_first_action_obj 
| limit 1 
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_first_action_obj = to_json_string(array_of_json_objects) -> [0]{} 
| fields event_id, array_of_json_objects, extracted_first_action_obj 
| limit 1
```

**Explanation**: The field `array_of_json_objects` contains an array of objects. The path `$[0]` (or `[0]{}`) extracts the first object in the array as a string.

**Output**:

| EVENT\_ID | ARRAY\_OF\_JSON\_OBJECTS                                            | EXTRACTED\_FIRST\_ACTION\_OBJ          |
| --------- | ------------------------------------------------------------------- | -------------------------------------- |
| 101       | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", ...}] | {"action": "read", "file": "doc1.txt"} |

### Example 4: Extracting the entire JSON field content (root extraction)

**Goal**: Extract the complete content of a JSON-formatted field as a string.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_full_json = json_extract(to_json_string(simple_json_data), "$") 
| fields event_id, simple_json_data, extracted_full_json 
| limit 1 
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter extracted_full_json = to_json_string(simple_json_data) -> {} 
| fields event_id, simple_json_data, extracted_full_json 
| limit 1
```

**Explanation**: Using `$` or `{}` with an empty string as the path signifies that the entire JSON content is to be extracted and returned.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA            | EXTRACTED\_FULL\_JSON         |
| --------- | ----------------------------- | ----------------------------- |
| 101       | {"status": "ok", "code": 200} | {"status": "ok", "code": 200} |

### Example 5: Extraction with a key containing special characters

**Goal**: Extract data when a key name contains special characters like a dot (`.`).

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| limit 1 
| alter json_with_special_key = to_string("{\"device.info\": {\"model\": \"XDR Agent\", \"version\": \"8.0\"}}") 
| alter extracted_special_key_obj = json_extract(json_with_special_key, "$['device.info']") 
| fields event_id, json_with_special_key, extracted_special_key_obj 
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| limit 1 
| alter json_with_special_key = to_string("{\"device.info\": {\"model\": \"XDR Agent\", \"version\": \"8.0\"}}") 
| alter extracted_special_key_obj = json_with_special_key -> ["device.info"]{} 
| fields event_id, json_with_special_key, extracted_special_key_obj 
```

**Explanation**: The key `device.info` contains a dot. In regular syntax, it is enclosed in single quotes and brackets `['device.info']`. In syntactic sugar, it uses double quotes and brackets `["device.info"]`.

**Output**:

| EVENT\_ID | JSON\_WITH\_SPECIAL\_KEY                                   | EXTRACTED\_SPECIAL\_KEY\_OBJ             |
| --------- | ---------------------------------------------------------- | ---------------------------------------- |
| 101       | {"device.info": {"model": "XDR Agent", "version": "8.0"\}} | {"model": "XDR Agent", "version": "8.0"} |

### Example 6: Handling a path that does not exist

**Goal**: Demonstrate behavior when the specified JSON path is not found.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 103 
| alter extracted_non_existent = json_extract(to_json_string(simple_json_data), "$.status") 
| fields event_id, simple_json_data, extracted_non_existent 
| limit 1 
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 103 
| alter extracted_non_existent = to_json_string(simple_json_data) -> status{} 
| fields event_id, simple_json_data, extracted_non_existent 
| limit 1
```

**Explanation**: For `event_id` 103, the `simple_json_data` field does not contain a `status` key. The function returns `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | EXTRACTED\_NON\_EXISTENT |
| --------- | ------------------------------------------------- | ------------------------ |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL                     |

### Example 7: Handling non-JSON formatted string input

**Goal**: Demonstrate behavior when the input is not valid JSON.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter non_json_input = event_description 
| alter result_from_non_json = json_extract(non_json_input, "$") 
| fields event_id, non_json_input, result_from_non_json 
| limit 1 
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter non_json_input = event_description 
| alter result_from_non_json = non_json_input -> {} 
| fields event_id, non_json_input, result_from_non_json 
| limit 1
```

**Explanation**: The `event_description` field is a plain string ("User login successful"), not a JSON structure. The function fails to parse it and returns `NULL`.

**Output**:

| EVENT\_ID | NON\_JSON\_INPUT        | RESULT\_FROM\_NON\_JSON |
| --------- | ----------------------- | ----------------------- |
| 101       | "User login successful" | NULL                    |

### Example 8: Using to\_json\_string() for explicit type conversion

**Goal**: Ensure input is a valid JSON string by explicitly converting a native object field.

**XQL code**:

#### Regular Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter nested_data_as_string = to_json_string(nested_json_data) 
| alter extracted_user_id = json_extract(nested_data_as_string, "$.user.id") 
| fields event_id, nested_json_data, nested_data_as_string, extracted_user_id 
| limit 1 
```

#### Syntactic Sugar Syntax

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter nested_data_as_string = to_json_string(nested_json_data) 
| alter extracted_user_id = nested_data_as_string -> user.id{} 
| fields event_id, nested_json_data, nested_data_as_string, extracted_user_id 
| limit 1
```

**Explanation**: The `nested_json_data` field is an object. `to_json_string()` is used to convert it into a valid JSON string required by `json_extract()`. The value "U1" is extracted as the string `"U1"`.

**Output**:

| EVENT\_ID | NESTED\_JSON\_DATA                           | NESTED\_DATA\_AS\_STRING                                 | EXTRACTED\_USER\_ID |
| --------- | -------------------------------------------- | -------------------------------------------------------- | ------------------- |
| 101       | {"user": {"id": "U1", "name": "Alice"}, ...} | {"user": {"id": "U1", "name": "Alice"}, ...} (as string) | ""U1""              |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`json_extract_scalar`](json_extract_scalar), [`json_extract_array`](json_extract_array), [`to_json_string`](to_json_string)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
