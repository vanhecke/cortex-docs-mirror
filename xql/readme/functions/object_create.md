# object\_create

Use the `object_create()` function to construct a new object by defining specific key-value pairs.

## Syntax

```sql
object_create ("<key1>", <value1>, "<key2>", <value2>, ...)
```

## Parameters

| Name      | Type                                           | Required | Description                                                                                                          |
| --------- | ---------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------- |
| `key_n`   | string                                         | Yes      | The name of the key. This must be a string literal enclosed in double quotes.                                        |
| `value_n` | string, integer, float, boolean, object, array | Yes      | The value associated with the preceding key. This can be a literal, a field name, or the result of another function. |

## Returns

The `object_create()` function returns a single object containing the specified key-value pairs.

## Usage notes

* The function requires an even number of arguments, structured as pairs of keys and values.
* All keys must be provided as string literals (enclosed in double quotes).
* Values can be of any XQL-supported data type, including strings, integers, floats, booleans, or results from other functions.
* The function does not implicitly convert string representations of numeric or boolean values; it retains the data types exactly as entered for the values.
* If a value parameter is `NULL`, the resulting object will typically contain a `NULL` value for that specific key.

## Examples

### Example 1: Creating an object with string literal key-value pairs

**Goal**: Construct an object using only string literals for both keys and values.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_metadata = object_create("source", "system_log", "level", "informational") 
| fields event_id, event_metadata 
| limit 3 
```

**Explanation**: This query adds a new field, `event_metadata`, containing a static object with two string key-value pairs for each record.

**Output**:

| EVENT\_ID | EVENT\_METADATA                                     |
| --------- | --------------------------------------------------- |
| 101       | {"source": "system\_log", "level": "informational"} |
| 102       | {"source": "system\_log", "level": "informational"} |
| 103       | {"source": "system\_log", "level": "informational"} |

### Example 2: Creating an object with mixed data type values (literals)

**Goal**: Construct an object that stores values of mixed data types (string, integer, boolean, float) using literal inputs.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_details = object_create( 
    "log_id_prefix", "XDR", 
    "priority_score", 100, 
    "is_critical", true, 
    "data_size_gb", 1.5 
  ) 
| fields event_id, event_details 
| limit 3 
```

**Explanation**: A new field `event_details` is created, holding an object where values are of different types (string, integer, boolean, float), demonstrating the function's flexibility in value data types.

**Output**:

| EVENT\_ID | EVENT\_DETAILS                                                                                  |
| --------- | ----------------------------------------------------------------------------------------------- |
| 101       | {"log\_id\_prefix": "XDR", "priority\_score": 100, "is\_critical": true, "data\_size\_gb": 1.5} |
| 102       | {"log\_id\_prefix": "XDR", "priority\_score": 100, "is\_critical": true, "data\_size\_gb": 1.5} |
| 103       | {"log\_id\_prefix": "XDR", "priority\_score": 100, "is\_critical": true, "data\_size\_gb": 1.5} |

### Example 3: Creating an object with existing field values

**Goal**: Construct an object using values pulled directly from existing fields in the dataset.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter contextual_info = object_create( 
    "event_type", event_description, 
    "success_status", is_successful, 
    "event_duration", duration_seconds, 
    "ip_address", ipv4_address 
  ) 
| fields event_id, event_description, is_successful, duration_seconds, ipv4_address, contextual_info 
| limit 3 
```

**Explanation**: The `contextual_info` field is populated with an object whose values are dynamically pulled from `event_description` (string), `is_successful` (boolean), `duration_seconds` (float), and `ipv4_address` (string) for each record.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | IS\_SUCCESSFUL | DURATION\_SECONDS | IPV4\_ADDRESS | CONTEXTUAL\_INFO                                                                                                              |
| --------- | -------------------------------- | -------------- | ----------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 101       | "User login successful"          | true           | 1.5               | 192.168.1.10  | {"event\_type": "User login successful", "success\_status": true, "event\_duration": 1.5, "ip\_address": "192.168.1.10"}      |
| 102       | "File access attempt"            | false          | 0.8               | 10.0.0.1      | {"event\_type": "File access attempt", "success\_status": false, "event\_duration": 0.8, "ip\_address": "10.0.0.1"}           |
| 103       | "Network connection established" | true           | 10.2              | 1.1.1.1       | {"event\_type": "Network connection established", "success\_status": true, "event\_duration": 10.2, "ip\_address": "1.1.1.1"} |

### Example 4: Creating an object with values from other functions

**Goal**: Construct an object using the output of other XQL functions (such as `len()` and `to_string()`) as values.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter derived_object = object_create( 
    "description_length", len(event_description), 
    "id_string", to_string(event_id) 
  ) 
| fields event_id, event_description, derived_object 
| limit 3 
```

**Explanation**: The `derived_object` contains the length of the `event_description` (an integer) and the string representation of `event_id`, obtained using `len()` and `to_string()` functions respectively.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | DERIVED\_OBJECT                                  |
| --------- | -------------------------------- | ------------------------------------------------ |
| 101       | "User login successful"          | {"description\_length": 23, "id\_string": "101"} |
| 102       | "File access attempt"            | {"description\_length": 20, "id\_string": "102"} |
| 103       | "Network connection established" | {"description\_length": 30, "id\_string": "103"} |

### Example 5: Handling NULL values in object\_create()

**Goal**: Demonstrate how the function handles `NULL` values provided for keys or values.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter null_handling_example = object_create( 
    "domain", dst_domain, 
    "static_null_value", NULL, // Explicit NULL value 
    "constant_key", "always_present" 
  ) 
| fields event_id, dst_domain, null_handling_example 
| limit 5 
```

**Explanation**: When `dst_domain` is `NULL` (as for event\_id 105), the "domain" key in the `null_handling_example` object also holds `NULL`. The "static\_null\_value" key consistently holds `NULL` due to its explicit `NULL` input. This demonstrates that `object_create()` will include `NULL` values for corresponding keys if the input value is `NULL`.

**Output**:

| EVENT\_ID | DST\_DOMAIN         | NULL\_HANDLING\_EXAMPLE                                                                          |
| --------- | ------------------- | ------------------------------------------------------------------------------------------------ |
| 101       | "ec2.amazonaws.com" | {"domain": "ec2.amazonaws.com", "static\_null\_value": NULL, "constant\_key": "always\_present"} |
| 102       | "sts.amazonaws.com" | {"domain": "sts.amazonaws.com", "static\_null\_value": NULL, "constant\_key": "always\_present"} |
| 103       | "www.google.com"    | {"domain": "www.google.com", "static\_null\_value": NULL, "constant\_key": "always\_present"}    |
| 104       | "dropbox.com"       | {"domain": "dropbox.com", "static\_null\_value": NULL, "constant\_key": "always\_present"}       |
| 105       | NULL                | {"domain": NULL, "static\_null\_value": NULL, "constant\_key": "always\_present"}                |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`object_merge`](object_merge)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
