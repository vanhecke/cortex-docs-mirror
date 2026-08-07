# object\_merge

Use the `object_merge()` function to construct a new object by merging the key-value pairs from two or more existing objects.

## Syntax

```sql
object_merge (<obj1>, <obj2>, <obj3>, ...)
```

## Parameters

| Name    | Type   | Required | Description                                 |
| ------- | ------ | -------- | ------------------------------------------- |
| `obj_n` | object | Yes      | Two or more object parameters to be merged. |

## Returns

The `object_merge()` function returns a single, new object containing the combined key-value pairs from the input objects.

## Usage notes

* When a key name is duplicated across multiple input objects, the value associated with that key in the new, merged object is determined by the value from the latter (rightmost) argument in the function call.
* If an entire object parameter provided to the function is `NULL`, the function effectively ignores that `NULL` input object and proceeds to merge the non-`NULL` objects.
* If a key within an input object has a `NULL` value, that `NULL` value is carried over into the merged object unless it is overridden by a subsequent object in the merge sequence that defines the same key.

## Examples

### Example 1: Merging two simple literal objects

**Goal**: Combine two objects created directly from literal key-value pairs to demonstrate basic merging and key override behavior.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter 
    obj1 = object_create("name", "jane", "last_name", "doe", "age", 33), 
    obj2 = object_create("name", "jane", "last_name", "simon", "age", 34, "city", "new-york") 
| alter result = object_merge(obj1, obj2) 
| fields event_id, result 
| limit 3
```

**Explanation**: The `result` object contains all unique keys from `obj1` and `obj2`. For `last_name` and `age`, the values from `obj2` ("simon", 34) overwrite those from `obj1` ("doe", 33) because `obj2` is the latter argument in the function.

**Output**:

| EVENT\_ID | RESULT                                                                 |
| --------- | ---------------------------------------------------------------------- |
| 101       | {"name": "jane", "last\_name": "simon", "age": 34, "city": "new-york"} |
| 102       | {"name": "jane", "last\_name": "simon", "age": 34, "city": "new-york"} |
| 103       | {"name": "jane", "last\_name": "simon", "age": 34, "city": "new-york"} |

### Example 2: Merging objects with overlapping keys and new keys

**Goal**: Demonstrate the "latter argument wins" rule for overlapping keys and the addition of new keys when merging three objects.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter 
    initial_security_status = object_create("alert_id", "A123", "status", "new", "severity", "medium"), 
    update_details = object_create("status", "in_progress", "analyst", "JohnDoe"), 
    final_disposition = object_create("status", "closed", "resolution", "false_positive") 
| alter combined_security_info = object_merge(initial_security_status, update_details, final_disposition) 
| fields event_id, combined_security_info 
| limit 3
```

**Explanation**: The `combined_security_info` object incorporates keys from all three input objects. The `status` key's value is "closed" from `final_disposition` because it is the latest object in the sequence to define that key. New keys like `analyst` and `resolution` are added without conflict.

**Output**:

| EVENT\_ID | COMBINED\_SECURITY\_INFO                                                                                               |
| --------- | ---------------------------------------------------------------------------------------------------------------------- |
| 101       | {"alert\_id": "A123", "status": "closed", "severity": "medium", "analyst": "JohnDoe", "resolution": "false\_positive"} |
| 102       | {"alert\_id": "A123", "status": "closed", "severity": "medium", "analyst": "JohnDoe", "resolution": "false\_positive"} |
| 103       | {"alert\_id": "A123", "status": "closed", "severity": "medium", "analyst": "JohnDoe", "resolution": "false\_positive"} |

### Example 3: Merging objects with values from existing dataset fields

**Goal**: Construct and merge objects using values pulled directly from existing fields in the dataset.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_summary_obj = object_create( 
    "description", event_description, 
    "successful", is_successful 
  ) 
| alter network_details_obj = object_create( 
    "ip_address", ipv4_address, 
    "domain", dst_domain 
  ) 
| alter full_event_context = object_merge(event_summary_obj, network_details_obj) 
| fields event_id, full_event_context 
| limit 3
```

**Explanation**: For each record, `event_summary_obj` captures the event's description and success status, while `network_details_obj` captures network-related fields. The function then combines these dynamically created objects into `full_event_context`.

**Output**:

| EVENT\_ID | FULL\_EVENT\_CONTEXT                                                                                                        |
| --------- | --------------------------------------------------------------------------------------------------------------------------- |
| 101       | {"description": "User login successful", "successful": true, "ip\_address": "192.168.1.10", "domain": "ec2.amazonaws.com"}  |
| 102       | {"description": "File access attempt", "successful": false, "ip\_address": "10.0.0.1", "domain": "sts.amazonaws.com"}       |
| 103       | {"description": "Network connection established", "successful": true, "ip\_address": "1.1.1.1", "domain": "www.google.com"} |

### Example 4: Merging objects with values derived from other functions

**Goal**: Use `object_merge()` where some of the object's key-value pairs are results of other XQL functions (for example, `to_string()`, `len()`).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter 
    event_ids_obj = object_create("event_id_str", to_string(event_id), "event_id_len", len(to_string(event_id))), 
    event_desc_obj = object_create("description_len", len(event_description)) 
| alter derived_and_merged_obj = object_merge(event_ids_obj, event_desc_obj) 
| fields event_id, derived_and_merged_obj 
| limit 3
```

**Explanation**: The `event_ids_obj` contains string and length properties derived from `event_id`. `event_desc_obj` contains the length of `event_description`. The function combines these, showcasing the ability to merge objects containing function-derived values.

**Output**:

| EVENT\_ID | DERIVED\_AND\_MERGED\_OBJ                                              |
| --------- | ---------------------------------------------------------------------- |
| 101       | {"event\_id\_str": "101", "event\_id\_len": 3, "description\_len": 23} |
| 102       | {"event\_id\_str": "102", "event\_id\_len": 3, "description\_len": 20} |
| 103       | {"event\_id\_str": "103", "event\_id\_len": 3, "description\_len": 30} |

### Example 5: Handling NULL object inputs during merge

**Goal**: Illustrate behavior when one of the input objects is `NULL`, demonstrating that `NULL` input objects are effectively ignored during the merge operation.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter 
    base_info = object_create("source_product", "Cortex XDR"), 
    // Conditional creation of 'dynamic_tag': 
    // If event_id / 2 equals its floor (i.e., event_id is even), create the object; otherwise, it is NULL. 
    conditional_info = if(divide(event_id, 2) = floor(divide(event_id, 2)), object_create("dynamic_tag", "processed"), NULL), 
    static_additional_info = object_create("processing_status", "completed") 
| alter merged_data_with_null = object_merge(base_info, conditional_info, static_additional_info) 
| fields event_id, merged_data_with_null 
| limit 5
```

**Explanation**: The `conditional_info` object is created only for records where `event_id` is even. For odd `event_id`s, `conditional_info` is `NULL`. In these instances, the function merges `base_info` and `static_additional_info`, skipping the `NULL` object. For even IDs, `conditional_info` is a valid object and its keys are included.

**Output**:

| EVENT\_ID | MERGED\_DATA\_WITH\_NULL                                                                          |
| --------- | ------------------------------------------------------------------------------------------------- |
| 101       | {"source\_product": "Cortex XDR", "processing\_status": "completed"}                              |
| 102       | {"source\_product": "Cortex XDR", "dynamic\_tag": "processed", "processing\_status": "completed"} |
| 103       | {"source\_product": "Cortex XDR", "processing\_status": "completed"}                              |
| 104       | {"source\_product": "Cortex XDR", "dynamic\_tag": "processed", "processing\_status": "completed"} |
| 105       | {"source\_product": "Cortex XDR", "processing\_status": "completed"}                              |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`object_create`](object_create)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
