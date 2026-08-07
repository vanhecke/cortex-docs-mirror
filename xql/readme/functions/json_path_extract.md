# json\_path\_extract

Use the `json_path_extract()` function to retrieve values from a JSON string based on a specified JSONPath expression.

## Syntax

```sql
json_path_extract (<json_field>, <json_path>)
```

## Parameters

| Name         | Type   | Required | Description                                                      |
| ------------ | ------ | -------- | ---------------------------------------------------------------- |
| `json_field` | string | Yes      | The field containing the JSON string from which to extract data. |
| `json_path`  | string | Yes      | The JSONPath expression identifying the data to extract.         |

## Returns

The `json_path_extract()` function returns a string representation of the extracted JSON data.

## Usage notes

* This function supports a syntactic sugar format for simplified query writing: `<json_field> ->-> "<json_path>"`.
* When using the regular syntax, the `<json_path>` must be enclosed in double quotes, and the root of the JSON object is represented by a dollar sign (`$`). The `$` is not required when using the syntactic sugar format.
* If a field name within the `<json_path>` contains special characters such as a dot (`.`) or colon (`:`), specific syntax is required:
* Regular Syntax: Enclose the field name in single quotes within brackets (for example, `['<json_field>']`).
* Syntactic Sugar Format: Enclose the field name in double quotes within brackets (for example, `["<json_field>"]`).
* JSON field names are case-sensitive. The key-to-field pairing in the XQL query must be identical to the JSON structure for results to be found.
* This function performs a "very heavy" operation and requires significant resources to run. Use it when standard dot-notation or simple array indexing is insufficient for your data extraction needs.
* The syntax used corresponds to the standard found in the JavaScript `jsonpath` package.

## Examples

### Example 1: Extracting all authors from a nested array

**Goal**: Extract all `author` values from the `ServerAccessConfig` array within the `Firewall` object using the `[*]` wildcard.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter all_authors = json_path_extract(json_field, "$.Firewall.ServerAccessConfig[*].author")
| fields event_id, all_authors
```

**Explanation**: The query defines a static JSON object and uses the `[*]` operator to iterate through all elements of the `ServerAccessConfig` array, extracting the `author` field from each.

**Output**:

| EVENT\_ID | ALL\_AUTHORS                               |
| --------- | ------------------------------------------ |
| 101       | \["NRees","EWaugh","HMelville","JTolkien"] |

### Example 2: Extracting authors with a specific priority

**Goal**: Use a filter expression within the JSONPath to find authors associated with a specific priority value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter specific_priority_author = json_path_extract(json_field, "$..*[?(@.priority==22.99)].author")
| fields event_id, specific_priority_author
```

**Explanation**: The query utilizes the filter expression `?(@.priority==22.99)` to match objects where the `priority` is exactly 22.99, and then extracts the `author` from those matching objects.

**Output**:

| EVENT\_ID | SPECIFIC\_PRIORITY\_AUTHOR |
| --------- | -------------------------- |
| 101       | \["JTolkien"]              |

### Example 3: Deep scan for all occurrences of a key

**Goal**: Use the recursive descent operator to find all `author` values anywhere in the JSON structure.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter all_authors_deep_scan = json_path_extract(json_field, "$..author")
| fields event_id, all_authors_deep_scan
```

**Explanation**: The query uses the `$..author` syntax to perform a deep scan of the entire JSON object, locating and extracting the value of every key named `author`, regardless of its nesting level.

**Output**:

| EVENT\_ID | ALL\_AUTHORS\_DEEP\_SCAN                   |
| --------- | ------------------------------------------ |
| 101       | \["NRees","EWaugh","HMelville","JTolkien"] |

### Example 4: Extracting all direct properties of an object

**Goal**: Extract all direct properties (keys and values) of a specific object using the wildcard operator.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter firewall_properties = json_path_extract(json_field, "$.Firewall.*")
| fields event_id, firewall_properties
```

**Explanation**: The query uses `$.Firewall.*` to retrieve all child elements (both the `ServerAccessConfig` array and the `Reviewer` object) directly under the `Firewall` key.

**Output**:

| EVENT\_ID | FIREWALL\_PROPERTIES                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 101       | \[\[{"category": "policy","author": "NRees","name": "CustomerSuccess\_NoAccess","priority": 8.95},{"category": "rule","author": "EWaugh","name": "AllowAccess\_10\_10\_10\_10","id": "0-553-21311-3","priority": 12.99},{"category": "policy","author": "HMelville","name": "SOC\_Access","priority": 8.99},{"category": "rule","author": "JTolkien","name": "AllowAccess\_JIT","id": "0-395-19395-8","priority": 22.99}],{"UserName": "jdow","Role": "Admin"}] |

### Example 5: Deep scan for specific keys

**Goal**: Use recursive descent to find all values associated with a specific key anywhere in the JSON.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter all_priorities = json_path_extract(json_field, "$.Firewall..priority")
| fields event_id, all_priorities
```

**Explanation**: The query uses `$.Firewall..priority` to recursively scan within the `Firewall` object and extract every value associated with the key `priority`.

**Output**:

| EVENT\_ID | ALL\_PRIORITIES          |
| --------- | ------------------------ |
| 101       | \[8.95,12.99,8.99,22.99] |

### Example 6: Extracting the last element of an array (length calculation)

**Goal**: Extract the last element of an array using the length property in a script expression.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter last_access_config_item = json_path_extract(json_field, "$..ServerAccessConfig[(@.length-1)]")
| fields event_id, last_access_config_item
```

**Explanation**: The query uses the script expression `(@.length-1)` to calculate the index of the last element in the `ServerAccessConfig` array and extract it.

**Output**:

| EVENT\_ID | LAST\_ACCESS\_CONFIG\_ITEM                                                                                      |
| --------- | --------------------------------------------------------------------------------------------------------------- |
| 101       | \[{"category": "rule","author": "JTolkien","name": "AllowAccess\_JIT","id": "0-395-19395-8","priority": 22.99}] |

### Example 7: Extracting the last element of an array (slice notation)

**Goal**: Extract the last element of an array using Python-style slice notation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter last_access_config_slice = json_path_extract(json_field, "$..ServerAccessConfig[-1:]")
| fields event_id, last_access_config_slice
```

**Explanation**: The query uses the slice notation `[-1:]` to grab the last item in the `ServerAccessConfig` array.

**Output**:

| EVENT\_ID | LAST\_ACCESS\_CONFIG\_SLICE                                                                                     |
| --------- | --------------------------------------------------------------------------------------------------------------- |
| 101       | \[{"category": "rule","author": "JTolkien","name": "AllowAccess\_JIT","id": "0-395-19395-8","priority": 22.99}] |

### Example 8: Extracting elements by specific indices

**Goal**: Extract multiple elements from an array by specifying their indices.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter first_two_configs_by_index = json_path_extract(json_field, "$..ServerAccessConfig[0,1]")
| fields event_id, first_two_configs_by_index
```

**Explanation**: The query targets the `ServerAccessConfig` array and uses `[0,1]` to extract only the first and second elements.

**Output**:

| EVENT\_ID | FIRST\_TWO\_CONFIGS\_BY\_INDEX                                                                                                                                                                                         |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 101       | \[{"category": "policy","author": "NRees","name": "CustomerSuccess\_NoAccess","priority": 8.95},{"category": "rule","author": "EWaugh","name": "AllowAccess\_10\_10\_10\_10","id": "0-553-21311-3","priority": 12.99}] |

### Example 9: Extracting a slice from the beginning of an array

**Goal**: Extract a range of elements from the start of an array using slice notation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| limit 1
| alter json_field = "{\"Firewall\":{\"ServerAccessConfig\":[{\"category\":\"policy\",\"author\":\"NRees\",\"name\":\"CustomerSuccess_NoAccess\",\"priority\":8.95},{\"category\":\"rule\",\"author\":\"EWaugh\",\"name\":\"AllowAccess_10_10_10_10\",\"id\":\"0-553-21311-3\",\"priority\":12.99},{\"category\":\"policy\",\"author\":\"HMelville\",\"name\":\"SOC_Access\",\"priority\":8.99},{\"category\":\"rule\",\"author\":\"JTolkien\",\"name\":\"AllowAccess_JIT\",\"id\":\"0-395-19395-8\",\"priority\":22.99}],\"Reviewer\":{\"UserName\":\"jdow\",\"Role\":\"Admin\"}}}"
| alter slice_from_beginning = json_path_extract(json_field, "$..ServerAccessConfig[:2]")
| fields event_id, slice_from_beginning
```

**Explanation**: The query uses `[:2]` to extract a slice of the `ServerAccessConfig` array starting from the beginning up to (but not including) index 2.

**Output**:

| EVENT\_ID | SLICE\_FROM\_BEGINNING                                                                                                                                                                                                 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 101       | \[{"category": "policy","author": "NRees","name": "CustomerSuccess\_NoAccess","priority": 8.95},{"category": "rule","author": "EWaugh","name": "AllowAccess\_10\_10\_10\_10","id": "0-553-21311-3","priority": 12.99}] |

### **Example 10: Extract data using different JSONPath expressions**

**Goal**: Define a JSON object called Firewall within a JSON field to illustrate multiple ways you can use the json\_path\_extract function to extract data using different JSONPath configurations.

**XQL Code**:

```sql
dataset = xdr_data | limit 1   
| alter  json_field = "{\"Firewall\": {\"ServerAccessConfig\": [{\"category\": \"policy\",\"author\": \"NRees\",\"name\": \"CustomerSuccess_NoAccess\",\"priority\": 8.95},{\"category\": \"rule\",\"author\": \"EWaugh\",\"name\": \"AllowAccess_10_10_10_10\",\"id\": \"0-553-21311-3\",\"priority\": 12.99},{\"category\": \"policy\",\"author\": \"HMelville\",\"name\": \"SOC_Access\",\"priority\": 8.99},{\"category\": \"rule\",\"author\": \"JTolkien\",\"name\": \"AllowAccess_JIT\",\"id\": \"0-395-19395-8\",\"priority\": 22.99}],\"Reviewer\": {\"UserName\": \"jdow\",\"Role\": \"Admin\"}}}"  
| alter a = json_path_extract(json_field, "$.Firewall.ServerAccessConfig[*].author")   
| alter b = json_path_extract(json_field, "$..*[?(@.priority==22.99)].author")   
| alter c = json_path_extract(json_field, "$..author")   
| alter d = json_path_extract(json_field, "$.Firewall.*")   
| alter e = json_path_extract(json_field, "$.Firewall..priority")   
| alter f = json_path_extract(json_field, "$..ServerAccessConfig[(@.length-1)]")   
| alter g = json_path_extract(json_field, "$..ServerAccessConfig[-1:]")   
| alter h = json_path_extract(json_field, "$..ServerAccessConfig[0,1]")   
| alter i = json_path_extract(json_field, "$..ServerAccessConfig[:2]")  
| fields json_field, a, b, c, d, e, f, g, h, i
```

**Explanation**: This query applies various JSONPath expressions to the json\_field to extract different sets of data. Here is how the different fields are configured:

* **a**: Outputs all of the values for the author key in the ServerAccessConfig JSON array.
* **b**: Outputs all of the values for the author key, where the value for the priority key is 22.99.
* **c**: Outputs all of the values for the author key anywhere found in the JSON.
* **d**: Outputs all of the values under the Firewall key.
* **e**: Outputs all of the values under the Firewall key for the priority key.
* **f**: Outputs the JSON array index value from the ServerAccessConfig JSON array according to its index location from the end of the array.
* **g**: Outputs all of the JSON array index values from the ServerAccessConfig JSON array according to its index location from the end of the array.
* **h**: Outputs a specific set of JSON array index values (one or more) from the ServerAccessConfig JSON array according to its index location.
* **i**: Outputs all of the JSON array index values from the ServerAccessConfig JSON array according to its index location from the start (0 Index) up to the mentioned index value.

**Output**:

| \_TIME                 | JSON\_FIELD                                                                                                                                                                                        | A                                  | B        | C                                  | D                                                                                                                                                                                    |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | -------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Jan 20th 2025 18:51:42 | {"Firewall": {"ServerAccessConfig": \[{"category": "policy", "author": "NRees", "name": "CustomerSuccess\_NoAccess", "priority": 8.95}, ...], "Reviewer": {"UserName": "jdow", "Role": "Admin"\}}} | NRees, EWaugh, HMelville, JTolkien | JTolkien | NRees, EWaugh, HMelville, JTolkien | {"ServerAccessConfig": \[{"category": "policy", "author": "NRees", "name": "CustomerSuccess\_NoAccess", "priority": 8.95}, ...], "Reviewer": {"UserName": "jdow", "Role": "Admin"\}} |

_Note: Columns E through I, \_PRODUCT, \_VENDOR, and INSERT\_TIMESTAMP are also returned by the query but omitted from this sample display for brevity._

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`json_extract`](json_extract), [`json_extract_array`](json_extract_array), [`json_extract_scalar`](json_extract_scalar), [`json_extract_scalar_array`](json_extract_scalar_array), [`to_json_string`](to_json_string)
