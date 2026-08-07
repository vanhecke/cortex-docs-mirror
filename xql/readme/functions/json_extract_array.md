# json\_extract\_array

Use the `json_extract_array()` function to accept a string that represents a JSON array and returns an XQL-native array. This function is crucial for transforming JSON-formatted array data into a format that XQL can natively process for further analysis.

## Syntax

**Regular syntax**

```sql
json_extract_array (<json_array_string>, <json_path>)
```

**Syntactic Sugar syntax**

```sql
<json_array_string> -> <json_path>[]
```

## Parameters

| Name                | Type   | Required | Description                                                                                                                                         |
| ------------------- | ------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `json_array_string` | string | Yes      | The string that represents a JSON array. To convert a field to a JSON-formatted string, use the `to_json_string()` function.                        |
| `json_path`         | string | Yes      | The argument that identifies the data of the JSON object you want to extract using dot-notation. In regular syntax, the root is represented by `$`. |

## Returns

The `json_extract_array()` function returns an XQL-native array.

## Usage notes

* The function requires a string that represents a JSON array as input.
* JSON field names are case-sensitive. The key-to-field pairing in your XQL query must be identical to the JSON for results to be found.
* When a field in the `<json_path>` contains special characters like a dot (`.`) or colon (`:`), specific syntax is required:
  * Regular Syntax\*\*: Use brackets with single quotes: `json_extract_array(<json_array_string>, "['<json_field>']")`.
  * Syntactic Sugar\*\*: Use brackets with double quotes: `<json_array_string> -> ["<json_field>"][]`.
* The `$` symbol representing the root of the JSON structure is required in the regular syntax but is not required in the syntactic sugar format.

## Examples

### Example 1: Extracting a root-level JSON array

**Goal**: Extract a direct JSON array from the `array_of_json_objects` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_array = json_extract_array(to_json_string(array_of_json_objects), "$") 
| fields event_id, array_of_json_objects, extracted_array 
| limit 2
```

**Explanation**: This query demonstrates extracting a direct JSON array. The syntactic sugar equivalent is `to_json_string(array_of_json_objects) -> []`.

**Output**:

| EVENT\_ID | ARRAY\_OF\_JSON\_OBJECTS                                                             | EXTRACTED\_ARRAY                                                                     |
| --------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| 101       | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}] | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}] |
| 102       | \[{"event": "file\_open", "path": "/etc/passwd"}]                                    | \[{"event": "file\_open", "path": "/etc/passwd"}]                                    |

### Example 2: Extracting a nested array with special characters in key

**Goal**: Extract an array where a key in the path contains a special character (a dot), demonstrating proper escaping.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_ips = json_extract_array(to_json_string(json_with_nested_array), "$['device.info']['ip.addresses']") 
| fields event_id, json_with_nested_array, extracted_ips 
| limit 2
```

**Explanation**: The `device.info` and `ip.addresses` keys are enclosed in single quotes within brackets (`['device.info']['ip.addresses']`) because they contain a dot, as per XQL syntax rules for regular JSON path. The syntactic sugar equivalent is `to_json_string(json_with_nested_array) -> ["device.info"]["ip.addresses"][]`.

**Output**:

| EVENT\_ID | JSON\_WITH\_NESTED\_ARRAY                                         | EXTRACTED\_IPS                |
| --------- | ----------------------------------------------------------------- | ----------------------------- |
| 101       | {"device.info": {"ip.addresses": \["172.16.6.7", "172.16.8.9"]\}} | \["172.16.6.7", "172.16.8.9"] |
| 102       | {"device.info": {"ip.addresses": \["10.1.2.3", "10.2.3.4"]\}}     | \["10.1.2.3", "10.2.3.4"]     |

### Example 3: Extracting an XQL numeric array converted to JSON string

**Goal**: Convert a native XQL array (`numeric_codes`) to a JSON string and then extract the entire array back.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_numeric = json_extract_array(to_json_string(numeric_codes), "$") 
| fields event_id, numeric_codes, extracted_numeric 
| limit 2
```

**Explanation**: The query converts the native array to a JSON string and then extracts it. The syntactic sugar equivalent is `to_json_string(numeric_codes) -> []`.

**Output**:

| EVENT\_ID | NUMERIC\_CODES          | EXTRACTED\_NUMERIC      |
| --------- | ----------------------- | ----------------------- |
| 101       | \[13, -47, 29, 82, -15] | \[13, -47, 29, 82, -15] |
| 102       | \[-21, 56, 13, -88, 42] | \[-21, 56, 13, -88, 42] |

### Example 4: Demonstrating XQL-native array output and element access

**Goal**: Showcase that `json_extract_array()` returns an XQL-native array that can be manipulated by other array functions like `arrayindex()`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter ip_addresses_array = to_json_string(json_with_nested_array) -> ["device.info"]["ip.addresses"][]
| alter first_ip = arrayindex(ip_addresses_array, 0) 
| fields event_id, json_with_nested_array, ip_addresses_array, first_ip 
| limit 2
```

**Explanation**: The `ip_addresses_array` is successfully extracted as an XQL-native array using `json_extract_array()` (syntactic sugar syntax used here). Subsequently, `arrayindex()` is used to retrieve the first element from this XQL-native array.

**Output**:

| EVENT\_ID | JSON\_WITH\_NESTED\_ARRAY                                         | IP\_ADDRESSES\_ARRAY          | FIRST\_IP    |
| --------- | ----------------------------------------------------------------- | ----------------------------- | ------------ |
| 101       | {"device.info": {"ip.addresses": \["172.16.6.7", "172.16.8.9"]\}} | \["172.16.6.7", "172.16.8.9"] | "172.16.6.7" |
| 102       | {"device.info": {"ip.addresses": \["10.1.2.3", "10.2.3.4"]\}}     | \["10.1.2.3", "10.2.3.4"]     | "10.1.2.3"   |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields)
* **Functions**: [`to_json_string`](to_json_string), [`arrayindex`](arrayindex)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
