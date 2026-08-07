# len

Use the `len()` function to return the number of characters contained in a specified string.

## Syntax

```sql
len (<string>)
```

## Parameters

| Name       | Type   | Required | Description                                       |
| ---------- | ------ | -------- | ------------------------------------------------- |
| `<string>` | string | Yes      | The string field or literal you want to evaluate. |

## Returns

The `len()` function returns an integer representing the count of characters.

## Usage notes

* If the input string is empty (`""`), `len()` will return `0`.
* If a `NULL` value is passed to `len()`, the function will return `NULL`.
* This function is typically used within the `alter` stage to create new fields or modify existing ones by calculating string lengths.
* The function can also be used in `filter` stages to narrow down results based on string length.

## Examples

### Example 1: Calculating the length of an existing string field

**Goal**: Calculate the character count of an existing string field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter description_length = len(event_description)
| fields event_id, event_description, description_length
| limit 3
```

**Explanation**: This query creates a new field, `description_length`, by calculating the character count of each `event_description`.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | DESCRIPTION\_LENGTH |
| --------- | -------------------------------- | ------------------- |
| 101       | "User login successful"          | 23                  |
| 102       | "File access attempt"            | 20                  |
| 103       | "Network connection established" | 30                  |

### Example 2: Calculating the length of a literal string

**Goal**: Calculate the length of a direct string literal provided in the query.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter literal_length = len("Palo Alto Networks")
| fields event_id, literal_length
| limit 3
```

**Explanation**: This query adds a new field, `literal_length`, which contains the constant length of the string "Palo Alto Networks" (18 characters, including spaces).

**Output**:

| EVENT\_ID | LITERAL\_LENGTH |
| --------- | --------------- |
| 101       | 18              |
| 102       | 18              |
| 103       | 18              |

### Example 3: Calculating the length of a string derived from a numerical field

**Goal**: Calculate the length of a numerical field by first converting it to a string.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_string = to_string(event_id)
| alter id_string_length = len(event_id_string)
| fields event_id, event_id_string, id_string_length
| limit 3
```

**Explanation**: This query first converts the numerical `event_id` to its string representation (for example, `101` becomes `"101"`) and then calculates the length of that string.

**Output**:

| EVENT\_ID | EVENT\_ID\_STRING | ID\_STRING\_LENGTH |
| --------- | ----------------- | ------------------ |
| 101       | "101"             | 3                  |
| 102       | "102"             | 3                  |
| 103       | "103"             | 3                  |

### Example 4: Calculating the length of a string extracted from JSON data

**Goal**: Extract a string value from a JSON field and calculate its length.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter status_string = simple_json_data -> status
| alter status_length = len(status_string)
| fields event_id, simple_json_data, status_string, status_length
| limit 3
```

**Explanation**: This query extracts the `status` value from `simple_json_data` as a string and then finds its length. For event\_id 103, because `simple_json_data` does not contain a `status` key, `status_string` becomes `NULL`, and subsequently, `status_length` also becomes `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | STATUS\_STRING | STATUS\_LENGTH |
| --------- | ------------------------------------------------- | -------------- | -------------- |
| 101       | {"status": "ok", "code": 200}                     | "ok"           | 2              |
| 102       | {"status": "fail", "error": "access\_denied"}     | "fail"         | 4              |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL           | NULL           |

### Example 5: Handling empty strings and NULL values

**Goal**: Demonstrate the behavior of the function with empty strings and NULL inputs.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter empty_string_test = ""
| alter empty_string_length = len(empty_string_test)
| alter dst_domain_length = len(dst_domain)
| fields event_id, empty_string_test, empty_string_length, dst_domain, dst_domain_length
| limit 5
```

**Explanation**: For all events, `empty_string_test` is an empty string, so `empty_string_length` is `0`. For event\_id 105, `dst_domain` is `NULL`, resulting in `dst_domain_length` also being `NULL`. For other events with non-NULL `dst_domain`, their respective string lengths are calculated.

**Output**:

| EVENT\_ID | EMPTY\_STRING\_TEST | EMPTY\_STRING\_LENGTH | DST\_DOMAIN         | DST\_DOMAIN\_LENGTH |
| --------- | ------------------- | --------------------- | ------------------- | ------------------- |
| 101       | ""                  | 0                     | "ec2.amazonaws.com" | 19                  |
| 102       | ""                  | 0                     | "sts.amazonaws.com" | 19                  |
| 103       | ""                  | 0                     | "www.google.com"    | 14                  |
| 104       | ""                  | 0                     | "dropbox.com"       | 11                  |
| 105       | ""                  | 0                     | NULL                | NULL                |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`to_string`](to_string), [`json_extract_scalar`](json_extract_scalar)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
