# to\_string

Use the `to_string()` function to convert a non-string value (such as a number, float, or boolean) into its string representation.

## Syntax

```sql
to_string (<field>)
```

## Parameters

| Name    | Type                    | Required | Description                                                      |
| ------- | ----------------------- | -------- | ---------------------------------------------------------------- |
| `field` | integer, float, boolean | Yes      | The field or literal value that you wish to convert to a string. |

## Returns

The `to_string()` function returns a string data type.

## Usage notes

* The function supports converting numerical types (integers and floats) and boolean values into strings.
* If the input field or literal is `NULL`, the function returns `NULL`.
* This function is essential when a string input is required for other XQL functions (like `concat()`, `format_string()`, or `split()`) or for performing string-based comparisons in `filter` stages.

## Examples

### Example 1: Converting a numeric (integer) field

**Goal**: Convert an integer field (`event_id`) to its string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter converted_event_id = to_string(event_id)
| fields event_id, converted_event_id
| limit 3
```

**Explanation**: The numeric `event_id` (for example, `101`) is successfully converted by `to_string()` into the string `"101"`.

**Output**:

| EVENT\_ID | CONVERTED\_EVENT\_ID |
| --------- | -------------------- |
| 101       | "101"                |
| 102       | "102"                |
| 103       | "103"                |

### Example 2: Converting a numeric (float) field

**Goal**: Convert a floating-point field (`duration_seconds`) to its string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter converted_duration = to_string(duration_seconds)
| fields event_id, duration_seconds, converted_duration
| limit 3
```

**Explanation**: The floating-point `duration_seconds` (for example, `1.5`) is converted by `to_string()` into the string `"1.5"`.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | CONVERTED\_DURATION |
| --------- | ----------------- | ------------------- |
| 101       | 1.5               | "1.5"               |
| 102       | 0.8               | "0.8"               |
| 103       | 10.2              | "10.2"              |

### Example 3: Converting a boolean field

**Goal**: Convert a boolean field (`is_successful`) to its string representation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter converted_status = to_string(is_successful)
| fields event_id, is_successful, converted_status
| limit 3
```

**Explanation**: The boolean `is_successful` value (for example, `true`) is converted by `to_string()` into the string `"true"`.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | CONVERTED\_STATUS |
| --------- | -------------- | ----------------- |
| 101       | true           | "true"            |
| 102       | false          | "false"           |
| 103       | true           | "true"            |

### Example 4: Converting a literal numeric value

**Goal**: Convert a literal integer and a literal float to their string representations.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter literal_int_to_string = to_string(99)
| alter literal_float_to_string = to_string(3.14)
| fields event_id, literal_int_to_string, literal_float_to_string
| limit 3
```

**Explanation**: Both the integer `99` and the float `3.14` are directly converted into their respective string representations.

**Output**:

| EVENT\_ID | LITERAL\_INT\_TO\_STRING | LITERAL\_FLOAT\_TO\_STRING |
| --------- | ------------------------ | -------------------------- |
| 101       | "99"                     | "3.14"                     |
| 102       | "99"                     | "3.14"                     |
| 103       | "99"                     | "3.14"                     |

### Example 5: Using `to_string()` in a filter condition

**Goal**: Convert a field to a string to enable string-based comparison in a filter stage.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter to_string(event_id) = "101"
| fields event_id, event_description, is_successful
| limit 3
```

**Explanation**: The `event_id` field is converted to a string before being compared to the string literal `"101"`, successfully filtering for the event with ID 101.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      | IS\_SUCCESSFUL |
| --------- | ----------------------- | -------------- |
| 101       | "User login successful" | true           |

### Example 6: Handling `NULL` input field

**Goal**: Demonstrate the behavior when the input field is explicitly NULL.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id = 105
| alter null_input_field = dst_domain
| alter converted_null = to_string(null_input_field)
| fields event_id, dst_domain, converted_null
| limit 1
```

**Explanation**: When the input to `to_string()` is `NULL` (for example, `dst_domain` for event ID 105), the function consistently returns `NULL`.

**Output**:

| EVENT\_ID | DST\_DOMAIN | CONVERTED\_NULL |
| --------- | ----------- | --------------- |
| 105       | NULL        | NULL            |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields)
* **Functions**: [`concat`](concat), [`format_string`](format_string), [`split`](split)
