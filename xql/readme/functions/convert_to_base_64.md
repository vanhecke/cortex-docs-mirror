# convert\_to\_base\_64

Use the `convert_to_base_64()` function to encode an input string into its base64 representation.

## Syntax

```sql
convert_to_base_64 ("<input_string>")
```

## Parameters

| Name           | Type   | Required | Description                      |
| -------------- | ------ | -------- | -------------------------------- |
| `input_string` | string | Yes      | The string to be base64 encoded. |

## Returns

The `convert_to_base_64()` function returns the base64-encoded value as a string.

## Usage notes

* The function requires a single string input.
* The function will return `NULL` if the input is `NULL`.
* This function is typically employed within the `alter` stage to create new fields or modify existing ones by encoding string data.
* The function can also be used within a `filter` stage if the encoding result is needed for a conditional check.

## Examples

### Example 1: Encoding a basic literal string

**Goal**: Encode a simple literal string to its base64 representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter encoded_string = convert_to_base_64("Hello world")
| fields event_id, encoded_string
| limit 3
```

**Explanation**: This query adds a new field, `encoded_string`, which contains the base64-encoded representation of "Hello world".

**Output**:

| EVENT\_ID | ENCODED\_STRING  |
| --------- | ---------------- |
| 101       | SGVsbG8gd29ybGQ= |
| 102       | SGVsbG8gd29ybGQ= |
| 103       | SGVsbG8gd29ybGQ= |

### Example 2: Encoding an existing string field

**Goal**: Encode values from an existing string field in the dataset.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter encoded_description = convert_to_base_64(event_description)
| fields event_id, event_description, encoded_description
| limit 3
```

**Explanation**: The query creates `encoded_description` by applying base64 encoding to the `event_description` field for each record.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             | ENCODED\_DESCRIPTION                     |
| --------- | ------------------------------ | ---------------------------------------- |
| 101       | User login successful          | VXNlciBsb2dpbiBzdWNjZXNzZnVs             |
| 102       | File access attempt            | RmlsZSBhY2Nlc3MgYXR0ZW1wdA==             |
| 103       | Network connection established | TmV0d29yayBjb25uZWN0aW9uIGVzdGFibGlzaGVk |

### Example 3: Encoding a string derived from a numeric field

**Goal**: Convert a numeric field to a string and then encode it to base64.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_string = to_string(event_id)
| alter encoded_id = convert_to_base_64(event_id_string)
| fields event_id, event_id_string, encoded_id
| limit 3
```

**Explanation**: The `event_id` is first converted to a string using `to_string()`, and then `convert_to_base_64()` encodes this string.

**Output**:

| EVENT\_ID | EVENT\_ID\_STRING | ENCODED\_ID |
| --------- | ----------------- | ----------- |
| 101       | 101               | MTAx        |
| 102       | 102               | MTAy        |
| 103       | 103               | MTAz        |

### Example 4: Encoding an empty string

**Goal**: Encode an empty string to observe the result.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter encoded_empty_string = convert_to_base_64("")
| fields event_id, encoded_empty_string
| limit 3
```

**Explanation**: Encoding an empty string results in an empty string.

**Output**:

| EVENT\_ID | ENCODED\_EMPTY\_STRING |
| --------- | ---------------------- |
| 101       |                        |
| 102       |                        |
| 103       |                        |

### Example 5: Handling NULL input

**Goal**: Observe the behavior when a NULL input is provided to the function.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter encoded_null_field = convert_to_base_64(dst_domain)
| fields event_id, dst_domain, encoded_null_field
| limit 5
```

**Explanation**: When the input to `convert_to_base_64()` is `NULL` (such as `dst_domain` for event 105), the function consistently returns `NULL` for the output field.

**Output**:

| EVENT\_ID | DST\_DOMAIN       | ENCODED\_NULL\_FIELD     |
| --------- | ----------------- | ------------------------ |
| 101       | ec2.amazonaws.com | ZWMyLmFtYXpvbmF3cy5jb20= |
| 102       | sts.amazonaws.com | c3RzLmFtYXpvbmF3cy5jb20= |
| 103       | www.google.com    | d3d3Lmdvb2dsZS5jb20=     |
| 104       | dropbox.com       | ZHJvcGJveC5jb20=         |
| 105       | NULL              | NULL                     |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields)
* **Functions**: [`convert_from_base_64`](convert_from_base_64), [`to_string`](to_string)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
