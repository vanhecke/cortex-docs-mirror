# json\_extract\_scalar

Use the `json_extract_scalar()` function to retrieve a single, atomic value—such as a string, number, or boolean—from a JSON object.

## Syntax

```sql
json_extract_scalar (<json_object_formatted_string>, <json_path>)
```

**Syntactic Sugar syntax**

```sql
<json_object_formatted_string> -> <field_path>
```

## Parameters

| Name                           | Type   | Required | Description                                                                                          |
| ------------------------------ | ------ | -------- | ---------------------------------------------------------------------------------------------------- |
| `json_object_formatted_string` | string | Yes      | The string representation of the JSON object.                                                        |
| `json_path`                    | string | Yes      | The path to the specific scalar value to extract, typically starting with `$` to represent the root. |

## Returns

The `json_extract_scalar()` function returns the extracted value as a string. If the targeted JSON field is an object or an array, or if the path does not exist, the function returns `NULL`.

## Usage notes

* The input `<json_object_formatted_string>` must be a string representation of a JSON object. You may need to use `to_json_string()` to convert fields like `nested_json_data` before extraction.
* This function always returns the extracted value as a string. To use the value as a number or boolean, you must chain functions like `to_integer()`, `to_float()`, or `to_boolean()`.
* JSON field names are case-sensitive. The key in your `json_path` must match the case in the JSON object exactly.
* XQL supports a "syntactic sugar" format for this function: `<json_object_formatted_string> -> <field_path>`. In this format, the leading `$` is not required.
* When a field name within the `<json_path>` contains special characters like a dot (`.`) or colon (`:`):
  * In **regular syntax**, enclose the field in single quotes within brackets: json\_extract\_scalar(\<json\_object\_formatted\_string>, "\['\<json\_field>']").
  * In **Syntactic Sugar syntax**, enclose the field in double quotes within brackets: \<json\_object\_formatted\_string> -> \["\<json\_field>"].

## Examples

### Example 1: Extracting a top-level string scalar value (status)

**Goal**: Extract a simple string value directly from the `simple_json_data` field using both regular syntax and syntactic sugar.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_status = json_extract_scalar(to_json_string(simple_json_data), "$.status") 
| fields event_id, simple_json_data, extracted_status 
| limit 2 
```

**Explanation**: This query converts `simple_json_data` to a JSON string and extracts the value associated with the "status" key.

**Output**:

| event\_id | simple\_json\_data                            | extracted\_status |
| --------- | --------------------------------------------- | ----------------- |
| 101       | {"status": "ok", "code": 200}                 | "ok"              |
| 102       | {"status": "fail", "error": "access\_denied"} | "fail"            |

### Example 2: Extracting a numeric scalar value (code) and converting to integer

**Goal**: Extract a numeric value (which returns as a string) and explicitly convert it to an integer.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_code_str = json_extract_scalar(to_json_string(simple_json_data), "$.code") 
| alter extracted_code_int = to_integer(extracted_code_str) 
| fields event_id, simple_json_data, extracted_code_str, extracted_code_int 
| limit 2 
```

**Explanation**: For event 101, the code "200" is extracted as a string and then converted to the integer 200. For event 102, the code field does not exist, so NULL is returned.

**Output**:

| event\_id | simple\_json\_data                            | extracted\_code\_str | extracted\_code\_int |
| --------- | --------------------------------------------- | -------------------- | -------------------- |
| 101       | {"status": "ok", "code": 200}                 | "200"                | 200                  |
| 102       | {"status": "fail", "error": "access\_denied"} | NULL                 | NULL                 |

### Example 3: Extracting a nested string scalar value (user.name)

**Goal**: Traverse a nested JSON structure to extract a specific scalar value.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_username = json_extract_scalar(to_json_string(nested_json_data), "$.user.name") 
| fields event_id, nested_json_data, extracted_username 
| limit 2 
```

**Explanation**: For event 101, the query navigates to `user.name` and extracts "Alice". For event 102, the user object is not present, resulting in NULL.

**Output**:

| event\_id | nested\_json\_data                                 | extracted\_username |
| --------- | -------------------------------------------------- | ------------------- |
| 101       | {"user": {"id": "U1", "name": "Alice"}, ...}       | "Alice"             |
| 102       | {"process": {"name": "cmd.exe", "pid": 1234}, ...} | NULL                |

### Example 4: Handling special characters in nested key names

**Goal**: Extract a value where the key name contains a special character (a dot), requiring specific bracket notation.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| limit 1 
| alter test_json_data = to_json_string("{\"a.b\": {\"scalar_field\": \"Special Value\"}}") 
| alter extracted_special_char_regular = json_extract_scalar(test_json_data, "$['a.b'].scalar_field") 
| fields event_id, test_json_data, extracted_special_char_regular 
```

**Explanation**: The key `'a.b'` is enclosed in single quotes within brackets `['a.b']` because it contains a dot, adhering to XQL's regular JSON path rules.

**Output**:

| event\_id | test\_json\_data                             | extracted\_special\_char\_regular |
| --------- | -------------------------------------------- | --------------------------------- |
| 101       | {"a.b": {"scalar\_field": "Special Value"\}} | "Special Value"                   |

### Example 5: Attempting to extract an object or array (returns NULL)

**Goal**: Demonstrate that the function returns NULL when the targeted path points to a complex structure (object or array) instead of a scalar.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_array_as_scalar = json_extract_scalar(to_json_string(array_of_json_objects), "$") 
| fields event_id, array_of_json_objects, extracted_array_as_scalar 
| limit 2 
```

**Explanation**: Attempting to extract the root `$` of `array_of_json_objects` (which is an array) using `json_extract_scalar` results in NULL because it is designed only for scalar values.

**Output**:

| event\_id | array\_of\_json\_objects        | extracted\_array\_as\_scalar |
| --------- | ------------------------------- | ---------------------------- |
| 101       | \[{"action": "read", ...}]      | NULL                         |
| 102       | \[{"event": "file\_open", ...}] | NULL                         |

### Example 6: Handling non-existent paths (returns NULL)

**Goal**: Demonstrate the behavior when the specified JSON path does not exist in the object.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_non_existent = json_extract_scalar(to_json_string(simple_json_data), "$.nonExistentField") 
| fields event_id, simple_json_data, extracted_non_existent 
| limit 2 
```

**Explanation**: Because `nonExistentField` is not present in the JSON structure, the function gracefully returns NULL.

**Output**:

| event\_id | simple\_json\_data                            | extracted\_non\_existent |
| --------- | --------------------------------------------- | ------------------------ |
| 101       | {"status": "ok", "code": 200}                 | NULL                     |
| 102       | {"status": "fail", "error": "access\_denied"} | NULL                     |

### Example 7: Filtering using an XQL-native datatype

**Goal**: Return the storage\_device\_drive\_type value from the action\_file\_device\_info field, and return the record if it is 1.

**XQL code**:

```sql
dataset = xdr_data   
| fields action_file_device_info as afdi   
| alter sdn = to_integer(json_extract_scalar(to_json_string(afdi), "$.storage_device_drive_type"))   
| filter sdn = 1   
| limit 10
```

**Explanation**: This query converts the action\_file\_device\_info object to a JSON string using to\_json\_string(), and then uses json\_extract\_scalar() to extract the storage\_device\_drive\_type value. Because the extraction returns a string, to\_integer() is used to cast the value into an XQL-native integer datatype before the filter stage evaluates if the value equals 1.

**Output**:

| AFDI                                                     | SDN |
| -------------------------------------------------------- | --- |
| {"storage\_device\_drive\_type": 1, "vendor": "SanDisk"} | 1   |
| {"storage\_device\_drive\_type": 1, "vendor": "Samsung"} | 1   |

### Example 8: Filtering using a string

**Goal**: Return the storage\_device\_drive\_type value from the action\_file\_device\_info field, and return the record if it matches the string value of "1".

**XQL code**:

```sql
dataset = xdr_data   
| fields action_file_device_info as afdi   
| alter sdn = json_extract_scalar(to_json_string(afdi), "$.storage_device_drive_type")   
| filter sdn = "1"   
| limit 10
```

**Explanation**: Similar to the first example, this query extracts the storage\_device\_drive\_type value as a string. However, instead of converting the datatype, the filter stage evaluates the result directly against the string literal "1".

**Output**:

| AFDI                                                       | SDN |
| ---------------------------------------------------------- | --- |
| {"storage\_device\_drive\_type": "1", "vendor": "SanDisk"} | "1" |
| {"storage\_device\_drive\_type": "1", "vendor": "Samsung"} | "1" |

### Example 9: Filtering using Syntactic Sugar Format

**Goal**: Return the storage\_device\_drive\_type value from the action\_file\_device\_info field using the shorthand syntactic sugar format.

**XQL code**:

```sql
dataset = xdr_data  
| fields action_file_device_info as afdi  
| alter sdn = to_integer(to_json_string(afdi)->storage_device_drive_type)  
| filter sdn = 1  
| limit 10
```

**Explanation**: This query achieves the exact same result as Example 7 but utilizes the JSON extract operator (->) as syntactic sugar. This shorthand format replaces the explicit json\_extract\_scalar() function call, making the query more concise while still converting the extracted string to an integer for the final filter evaluation.

**Output**:

| AFDI                                                     | SDN |
| -------------------------------------------------------- | --- |
| {"storage\_device\_drive\_type": 1, "vendor": "SanDisk"} | 1   |
| {"storage\_device\_drive\_type": 1, "vendor": "Samsung"} | 1   |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`to_json_string`](to_json_string), [`to_integer`](to_integer), [`to_float`](to_float), [`to_boolean`](to_boolean)
