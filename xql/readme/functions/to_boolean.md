# to\_boolean

Use the `to_boolean()` function to explicitly transform string representations of boolean values into their native boolean data type.

## Syntax

```sql
to_boolean (<string>)
```

## Parameters

| Name     | Type   | Required | Description                                                 |
| -------- | ------ | -------- | ----------------------------------------------------------- |
| `string` | string | Yes      | The string field or literal value that you want to convert. |

## Returns

The `to_boolean()` function returns a boolean value (`true` or `false`).

## Usage notes

* The input string must be either "TRUE" or "FALSE".
* The conversion is case-insensitive, meaning "true", "TRUE", "True", "false", "FALSE", "False", etc., are all valid inputs for conversion.
* If the input string is not "TRUE" or "FALSE" (case-insensitive), or if the input is `NULL`, the function will return `NULL`.

## Examples

### Example 1: Converting a literal string "TRUE"

**Goal**: Convert the literal string "TRUE" to a boolean `true` value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter is_active_flag = to_boolean("TRUE")
| fields event_id, is_active_flag
| limit 3
```

**Explanation**: This query creates a new field, `is_active_flag`, which holds the boolean `true` value for every record, derived from the literal string "TRUE".

**Output**:

| EVENT\_ID | IS\_ACTIVE\_FLAG |
| --------- | ---------------- |
| 101       | true             |
| 102       | true             |
| 103       | true             |

### Example 2: Converting a literal string "FALSE"

**Goal**: Convert the literal string "FALSE" to a boolean `false` value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter is_blocked_flag = to_boolean("FALSE")
| fields event_id, is_blocked_flag
| limit 3
```

**Explanation**: This query creates a new field, `is_blocked_flag`, which holds the boolean `false` value for every record, derived from the literal string "FALSE".

**Output**:

| EVENT\_ID | IS\_BLOCKED\_FLAG |
| --------- | ----------------- |
| 101       | false             |
| 102       | false             |
| 103       | false             |

### Example 3: Converting a case-insensitive literal string

**Goal**: Convert mixed-case literal strings (for example, "true", "FaLsE") to their boolean equivalents.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter status_boolean_lower = to_boolean("true")
| alter status_boolean_mixed = to_boolean("FaLsE")
| fields event_id, status_boolean_lower, status_boolean_mixed
| limit 3
```

**Explanation**: The query demonstrates that `to_boolean()` successfully interprets both "true" and "FaLsE" (case-insensitively) into their respective boolean `true` and `false` values.

**Output**:

| EVENT\_ID | STATUS\_BOOLEAN\_LOWER | STATUS\_BOOLEAN\_MIXED |
| --------- | ---------------------- | ---------------------- |
| 101       | true                   | false                  |
| 102       | true                   | false                  |
| 103       | true                   | false                  |

### Example 4: Converting a derived string field

**Goal**: Convert a string field ("TRUE"/"FALSE") derived from existing data into a boolean type.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter success_string = if(is_successful = true, "TRUE", "FALSE")
| alter converted_success = to_boolean(success_string)
| fields event_id, is_successful, success_string, converted_success
| limit 3
```

**Explanation**: The `if()` function first creates `success_string` as either "TRUE" or "FALSE" based on `is_successful`. Then, `to_boolean()` correctly converts this string representation into a native boolean value in `converted_success`.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | SUCCESS\_STRING | CONVERTED\_SUCCESS |
| --------- | -------------- | --------------- | ------------------ |
| 101       | true           | "TRUE"          | true               |
| 102       | false          | "FALSE"         | false              |
| 103       | true           | "TRUE"          | true               |

### Example 5: Handling invalid string input

**Goal**: Demonstrate the behavior when attempting to convert an invalid string or a NULL value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter invalid_conversion = to_boolean("not_a_boolean_string")
| alter null_input_conversion = to_boolean(NULL)
| fields event_id, invalid_conversion, null_input_conversion
| limit 3
```

**Explanation**: As expected for invalid conversions in XQL, both attempts result in `NULL` values for the new fields, demonstrating `to_boolean()`'s strict input requirements.

**Output**:

| EVENT\_ID | INVALID\_CONVERSION | NULL\_INPUT\_CONVERSION |
| --------- | ------------------- | ----------------------- |
| 101       | NULL                | NULL                    |
| 102       | NULL                | NULL                    |
| 103       | NULL                | NULL                    |

### Example 6: Using supported operators for deriving a boolean string

**Goal**: Use `to_boolean()` within a `filter` stage to evaluate a derived string field as a boolean condition (for example, checking if an event ID is odd).

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter division_result = divide(event_id, 2)
| alter is_event_active_string = if(division_result != floor(division_result), "TRUE", "FALSE")
| filter to_boolean(is_event_active_string) = true
| fields event_id, is_event_active_string
| limit 3
```

**Explanation**: This query calculates the remainder of dividing `event_id` by 2. If the result is not a whole number (meaning the ID is odd), it assigns "TRUE" to the string field. `to_boolean()` converts this string to a boolean for the filter, returning only records with odd event IDs.

**Output**:

| EVENT\_ID | IS\_EVENT\_ACTIVE\_STRING |
| --------- | ------------------------- |
| 101       | "TRUE"                    |
| 103       | "TRUE"                    |
| 105       | "TRUE"                    |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`if`](if), [`divide`](divide), [`floor`](floor)
