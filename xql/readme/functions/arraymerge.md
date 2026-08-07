# arraymerge

Use the `arraymerge()` function to flatten an input array containing JSON strings representing arrays into a single, merged XQL array.

## Syntax

```sql
arraymerge (<field>)
```

## Parameters

| Name    | Type  | Required | Description                                                                                                                             |
| ------- | ----- | -------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `field` | array | Yes      | A single array field whose elements are JSON strings, where each JSON string represents an array (for example, `["value1", "value2"]`). |

## Returns

The `arraymerge()` function returns a new, flattened XQL-native array containing all elements from the inner JSON-string-represented arrays.

## Usage notes

* The function strictly requires an array where each element is a valid JSON string that represents an array.
* The function flattens the structure, taking an array of arrays (represented as JSON strings) and reducing it to a single-dimensional array.
* This function is commonly used in conjunction with `arraymap()` when the internal function of `arraymap()` produces JSON strings of arrays.

## Examples

### Example 1: Merging artificially constructed arrays (literal JSON strings)

**Goal**: Demonstrate the core functionality by creating an array where each element is a JSON string representing an array, and then flattening them into a single array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter json_array_str_part1 = to_json_string(arraycreate("tag1", "tag2")) // Creates JSON string '["tag1", "tag2"]' 
| alter json_array_str_part2 = to_json_string(arraycreate("valueA", "valueB")) // Creates JSON string '["valueA", "valueB"]' 
| alter input_array_for_merge = arraycreate(json_array_str_part1, json_array_str_part2) // Creates an array of these JSON strings: ['["tag1", "tag2"]', '["valueA", "valueB"]'] 
| alter merged_result = arraymerge(input_array_for_merge) 
| fields event_id, merged_result 
| limit 2 
```

**Explanation**: The query first creates two string representations of arrays (`json_array_str_part1` and `json_array_str_part2`) using `arraycreate()` and `to_json_string()`. The query then combines these into `input_array_for_merge`. Finally, `arraymerge()` extracts the elements from within each JSON string in the input array and combines them into a single, flattened `merged_result` array.

**Output**:

| EVENT\_ID | MERGED\_RESULT                        |
| --------- | ------------------------------------- |
| 101       | \["tag1", "tag2", "valueA", "valueB"] |
| 102       | \["tag1", "tag2", "valueA", "valueB"] |

### Example 2: Merging scalar values extracted and wrapped into arrays via arraymap()

**Goal**: Demonstrate how to process an array of JSON objects, extract specific scalar values, wrap them into new conceptual arrays, convert them to JSON strings, and finally flatten the result using `arraymerge()`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter mapped_json_arrays_as_strings = arraymap( 
    array_of_json_objects, 
    to_json_string( // Converts the dynamically created array into a JSON string 
        arraycreate( // Creates a new temporary array from extracted scalars 
            to_string(coalesce(json_extract_scalar(to_json_string("@element"), "$.action"), json_extract_scalar(to_json_string("@element"), "$.event"))), // Extracts 'action' or 'event' 
            to_string(coalesce(json_extract_scalar(to_json_string("@element"), "$.file"), json_extract_scalar(to_json_string("@element"), "$.path"), json_extract_scalar(to_json_string("@element"), "$.conn_type"))) // Extracts 'file', 'path', or 'conn_type' 
        ) 
    ) 
) 
| alter flattened_array = arraymerge(mapped_json_arrays_as_strings) 
| fields event_id, array_of_json_objects, flattened_array 
| limit 4 
```

**Explanation**: `arraymap()` iterates over each JSON object in `array_of_json_objects`. For each element, it extracts specific scalar values (like action, event, file, path) using `json_extract_scalar()` and wraps them into a temporary array using `arraycreate()`. `to_json_string()` converts this temporary array into a JSON string. The result of `arraymap()` is an array of these JSON strings. Finally, `arraymerge()` flattens all the inner elements from these strings into a single `flattened_array`.

**Output**:

| EVENT\_ID | ARRAY\_OF\_JSON\_OBJECTS                                                              | FLATTENED\_ARRAY                             |
| --------- | ------------------------------------------------------------------------------------- | -------------------------------------------- |
| 101       | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}]  | \["read", "doc1.txt", "write", "report.log"] |
| 102       | \[{"event": "file\_open", "path": "/etc/passwd"}]                                     | \["file\_open", "/etc/passwd"]               |
| 103       | \[{"conn\_type": "outbound", "bytes": 1024}, {"conn\_type": "inbound", "bytes": 512}] | \["outbound", "inbound"]                     |
| 104       | \[]                                                                                   | \[]                                          |

### Example 2: Merge IP addresses extracted from a nested map

**Goal**: Create a single consolidated array containing all IPv4 addresses found within the `agent_interface_map` field. This query extracts the "ipv4" element from each object in the map and merges them into a flattened array.

**XQL Code**:

```sql
dataset = sample_xql_raw
| alter a = arraymerge(arraymap(agent_interface_map, to_json_string(json_extract_array(to_json_string("@element"), "$.ipv4"))))
```

**Explanation**:

1. The query processes the agent\_interface\_map, which is an array of objects.
2. arraymap() iterates through each element (@element) in the array.
3. to\_json\_string() converts the element to a JSON string so it can be parsed.
4. json\_extract\_array(..., "$.ipv4") locates and extracts the IPv4 addresses associated with the "ipv4" key in each object.
5. arraymerge() takes the resulting nested arrays and flattens them into a single, comprehensive array assigned to the field 'a'.

**Output**:

| agent\_interface\_map                                                            | a                             |
| -------------------------------------------------------------------------------- | ----------------------------- |
| \[{"ipv4":\["10.0.0.1"],"name":"eth0"},{"ipv4":\["192.168.1.1"],"name":"wlan0"}] | \["10.0.0.1", "192.168.1.1"]  |
| \[{"ipv4":\["172.16.0.5", "172.16.0.6"],"name":"eth1"}]                          | \["172.16.0.5", "172.16.0.6"] |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`arraycreate`](arraycreate), [`to_json_string`](to_json_string), [`arraymap`](arraymap), [`json_extract_scalar`](json_extract_scalar), [`to_string`](to_string), [`coalesce`](coalesce)
