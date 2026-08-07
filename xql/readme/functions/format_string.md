# format\_string

Use the `format_string()` function to construct dynamic strings by inserting values into a predefined format.

## Syntax

```sql
format_string ("<format_string>", <field_1>, <field_2>, ...<field_n>)
```

## Parameters

| Name            | Type            | Required | Description                                                                                                                                                                            |
| --------------- | --------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `format_string` | string          | Yes      | A string literal that contains zero or more format specifiers initiated by the `%` symbol (for example, `%s`, `%d`).                                                                   |
| `field_n`       | string, integer | Yes      | A variable-length list of additional arguments whose values will be inserted into the format string. Each argument must match the type expected by its corresponding format specifier. |

## Returns

The `format_string()` function returns a single string containing the formatted text with argument values inserted.

## Usage notes

* Common format specifiers include `%s` for string values and `%d` for integer values.
* You can use padding and width specifiers (for example, `%10d`, `%05d`, `%-10s`) to control output alignment and formatting.
* The function requires strict type compatibility between arguments and specifiers. The function does not implicitly convert types (for example, a floating-point number passed to `%d` will fail).
* Use explicit type conversion functions like `to_string()` or `to_integer()` to ensure non-matching values (like booleans or floats) are compatible with the specifiers.
* Note that `to_number()` converts strings to floating-point numbers, which are incompatible with the `%d` (integer) specifier; use `to_integer()` instead.

## Examples

### Example 1: Basic string substitution (%s)

**Goal**: Combine literal text with string field values using the `%s` specifier.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_message = format_string("Description: %s. Domain: %s.", event_description, dst_domain)
| fields event_id, event_message
| limit 3
```

**Explanation**: The `event_description` and `dst_domain` fields, which are strings, are directly inserted into the format string at the `%s` placeholders.

**Output**:

| EVENT\_ID | EVENT\_MESSAGE                                                         |
| --------- | ---------------------------------------------------------------------- |
| 101       | "Description: User login successful. Domain: ec2.amazonaws.com."       |
| 102       | "Description: File access attempt. Domain: sts.amazonaws.com."         |
| 103       | "Description: Network connection established. Domain: www.google.com." |

### Example 2: Integer substitution (%d)

**Goal**: Embed integer field values into a string using the `%d` specifier.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter formatted_id = format_string("Event #%d occurred.", event_id)
| fields event_id, formatted_id
| limit 3
```

**Explanation**: The `event_id` (an integer) is converted to its string representation and inserted into the output string where `%d` is specified.

**Output**:

| EVENT\_ID | FORMATTED\_ID          |
| --------- | ---------------------- |
| 101       | "Event #101 occurred." |
| 102       | "Event #102 occurred." |
| 103       | "Event #103 occurred." |

### Example 3: Combining different data types

**Goal**: Combine values of different original data types (boolean, float) into a single formatted string using explicit conversion.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter detailed_status = format_string("Successful: %s, Duration: %s seconds", to_string(is_successful), to_string(duration_seconds))
| fields event_id, is_successful, duration_seconds, detailed_status
| limit 3
```

**Explanation**: `to_string(is_successful)` converts the boolean to "true" or "false". `to_string(duration_seconds)` converts the float to a string like "1.5". `format_string()` then constructs the final string using these string representations for the `%s` specifiers.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | DURATION\_SECONDS | DETAILED\_STATUS                           |
| --------- | -------------- | ----------------- | ------------------------------------------ |
| 101       | true           | 1.5               | "Successful: true, Duration: 1.5 seconds"  |
| 102       | false          | 0.8               | "Successful: false, Duration: 0.8 seconds" |
| 103       | true           | 10.2              | "Successful: true, Duration: 10.2 seconds" |

### Example 4: Padding and zero-padding for integers

**Goal**: Utilize padding specifiers with `%d` and `%s` to control width and alignment.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter padded_event_id = format_string("ID: %05d | Full ID: %-10s | Raw: %s", event_id, to_string(event_id), to_string(event_id))
| fields event_id, padded_event_id
| limit 3
```

**Explanation**: `%05d` pads `event_id` with leading zeros to a width of 5. `%-10s` left-justifies the string version within 10 characters. `%s` performs basic substitution.

**Output**:

| EVENT\_ID | PADDED\_EVENT\_ID |
| --------- | ----------------- |
| 101       | ID: 00101         |
| 102       | ID: 00101         |
| 103       | ID: 00101         |

### Example 5: Formatting extracted JSON scalar values with integer conversion

**Goal**: Extract a numeric string from JSON, convert it to an integer, and format it with `%d`.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter status_code_string = coalesce(simple_json_data -> code, simple_json_data -> error_code)
| alter status_int = to_integer(status_code_string)
| alter formatted_status = format_string("API Status: %d", status_int)
| fields event_id, simple_json_data, formatted_status
| limit 3
```

**Explanation**: The query extracts the code as a string and explicitly converts it to an integer using `to_integer()`. This ensures compatibility with the `%d` specifier, which would fail if a float (from `to_number`) were passed.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | FORMATTED\_STATUS |
| --------- | ------------------------------------------------- | ----------------- |
| 101       | {"status": "ok", "code": 200}                     | "API Status: 200" |
| 102       | {"status": "fail", "error": "access\_denied"}     | NULL              |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL              |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields)
* **Functions**: [`to_string`](to_string), [`to_integer`](to_integer), [`concat`](concat)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
