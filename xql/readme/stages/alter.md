# alter

Use the `alter` stage to manipulate data by changing existing field values or creating new fields based on constants, other fields, or the results of various XQL functions.

## Syntax

```sql
alter <field1> = <function value1> [, <field2> = <function_value2>, ...]
```

## Parameters

| Name               | Type    | Required | Description                                                               |
| ------------------ | ------- | -------- | ------------------------------------------------------------------------- |
| `<field>`          | string  | Yes      | The name of the field to create or modify.                                |
| `<function_value>` | various | Yes      | The constant, field reference, or function result to assign to the field. |

## Returns

The `alter` stage returns the dataset with the specified fields modified or added. New columns created by the `alter` stage are added as the last columns in the result set.

## Usage notes

* New fields and field values can only be created in the `alter` stage. No other stage allows for the creation of new fields and/or values.
* After defining or modifying a field with `alter`, you can apply other stages, such as `filter`, to this new or modified field.
* New columns created by the `alter` stage are added as the last columns in the result set. If a specific column order is desired, it can be adjusted using the `fields` stage later in the query.
* XQL supports single (`"<text>"`) and triple (`"""<text>"""`) double quotes for defining string fields.
* Single quotes treat values literally, while triple quotes process escape sequences (like `\t` for tab) and escaped backslashes. Choose the appropriate quoting based on your desired interpretation of special characters.

## Examples

### Example 1: Creating a new field with a constant value

**Goal**: Add a new column with a fixed value for all records.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter analysis_tag = "initial_review"
| fields event_id, analysis_tag
```

**Explanation**: A new field `analysis_tag` is created, and the value "initial\_review" is assigned to every record.

**Output**:

| EVENT\_ID | ANALYSIS\_TAG   |
| --------- | --------------- |
| 101       | initial\_review |
| 102       | initial\_review |
| 103       | initial\_review |

### Example 2: Creating a new field based on an existing field

**Goal**: Duplicate a field or create a new field that directly references an existing one.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter replicated_description = event_description
| fields event_id, replicated_description
```

**Explanation**: The `replicated_description` field is created, mirroring the `event_description` field.

**Output**:

| EVENT\_ID | REPLICATED\_DESCRIPTION        |
| --------- | ------------------------------ |
| 101       | User login successful          |
| 102       | File access attempt            |
| 103       | Network connection established |

### Example 3: Modifying an existing field

**Goal**: Overwrite the current value of a known field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_description = concat("Processed: ", event_description)
| fields event_id, event_description
```

**Explanation**: The original `event_description` is updated by prepending "Processed: " to its value.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION                        |
| --------- | ----------------------------------------- |
| 101       | Processed: User login successful          |
| 102       | Processed: File access attempt            |
| 103       | Processed: Network connection established |

### Example 4: Using string manipulation functions (concat)

**Goal**: Join multiple strings together to reformat text data.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_summary = concat(event_description, " - Success: ", to_string(is_successful))
| fields event_id, event_summary
```

_Explanation_\*: `event_summary` is created by concatenating the event description, a static string, and the boolean `is_successful` converted to a string.

**Output**:

| EVENT\_ID | EVENT\_SUMMARY                                 |
| --------- | ---------------------------------------------- |
| 101       | User login successful - Success: true          |
| 102       | File access attempt - Success: false           |
| 103       | Network connection established - Success: true |

### Example 5: Using string manipulation functions (lowercase)

**Goal**: Convert a string to all lowercase letters.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter lower_case_log = lowercase(raw_log_data)
| fields event_id, lower_case_log
```

**Explanation**: The `raw_log_data` field's content is converted to lowercase and stored in `lower_case_log`.

**Output**:

| EVENT\_ID | LOWER\_CASE\_LOG                                |
| --------- | ----------------------------------------------- |
| 101       | user alice logged in from 192.168.1.10          |
| 102       | process cmd.exe attempted to access /etc/passwd |

### Example 6: Using string manipulation functions (split)

**Goal**: Divide a string into an array of substrings based on a delimiter.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter log_words = split(raw_log_data, " ")
| fields event_id, log_words
```

**Explanation**: The `raw_log_data` string is split into an array of words based on spaces, creating the `log_words` field.

**Output**:

| EVENT\_ID | LOG\_WORDS                                                          |
| --------- | ------------------------------------------------------------------- |
| 101       | \["User", "Alice", "logged", "in", "from", "192.168.1.10"]          |
| 102       | \["Process", "cmd.exe", "attempted", "to", "access", "/etc/passwd"] |

### Example 7: Using JSON functions (json\_extract\_scalar)

**Goal**: Extract a single scalar value (for example, string, number, boolean) from a JSON object.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter json_status = json_extract_scalar(simple_json_data, "$.status")
| fields event_id, json_status
```

**Explanation**: Extracts the value of the "status" key from the `simple_json_data` JSON object into `json_status`.

**Output**:

| EVENT\_ID | JSON\_STATUS |
| --------- | ------------ |
| 101       | ok           |
| 102       | fail         |

### Example 8: Using JSON functions (json\_extract\_array)

**Goal**: Convert a JSON array string to an XQL-native array.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter parsed_actions = json_extract_array(array_of_json_objects, "$")
| fields event_id, parsed_actions
```

**Explanation**: Converts the `array_of_json_objects` string (which contains a JSON array) into a native XQL array stored in `parsed_actions`.

**Output**:

| EVENT\_ID | PARSED\_ACTIONS                                                                      |
| --------- | ------------------------------------------------------------------------------------ |
| 101       | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}] |
| 102       | \[{"event": "file\_open", "path": "/etc/passwd"}]                                    |

### Example 9: Using conditional and null handling functions (if)

**Goal**: Apply logic to assign values based on conditions.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter outcome_category = if(is_successful, "Operational", "Alertable")
| fields event_id, outcome_category
```

**Explanation**: If `is_successful` is true, creates `outcome_category` as "Operational". If `is_successful` is false, creates `outcome_category` as "Alertable".

**Output**:

| EVENT\_ID | OUTCOME\_CATEGORY |
| --------- | ----------------- |
| 101       | Operational       |
| 102       | Alertable         |
| 103       | Operational       |

### Example 10: Using conditional and null handling functions (coalesce)

**Goal**: Return the first non-NULL expression among its arguments.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter resolved_ip = coalesce(ipv4_address, ipv6_address)
| fields event_id, resolved_ip
```

**Explanation**: Assigns the value of `ipv4_address` to `resolved_ip`. If `ipv4_address` is NULL, the field is assigned `ipv6_address` instead.

**Output**:

| EVENT\_ID | RESOLVED\_IP |
| --------- | ------------ |
| 101       | 192.168.1.10 |
| 103       | 2001:0db8::1 |

### Example 11: Using time functions (format\_timestamp)

**Goal**: Format a timestamp into a specified string format.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter formatted_timestamp = format_timestamp("%Y-%m-%d %H:%M:%S", _time)
| fields event_id, formatted_timestamp
```

**Explanation**: Converts the `_time` field into a readable string format `YYYY-MM-DD HH:MM:SS`.

**Output**:

| EVENT\_ID | FORMATTED\_TIMESTAMP |
| --------- | -------------------- |
| 101       | 2023-10-26 10:00:00  |
| 102       | 2023-10-26 10:05:30  |

### Example 12: Using mathematical functions (add)

**Goal**: Add two numerical values.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter adjusted_duration = add(duration_seconds, 5.0)
| fields event_id, adjusted_duration
```

**Explanation**: Adds 5.0 to `duration_seconds` for each record, storing the result in `adjusted_duration`.

**Output**:

| EVENT\_ID | ADJUSTED\_DURATION |
| --------- | ------------------ |
| 101       | 6.5                |
| 102       | 5.8                |

### Example 13: Using mathematical functions (multiply)

**Goal**: Multiply two numerical values.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter doubled_duration = multiply(duration_seconds, 2)
| fields event_id, doubled_duration
```

**Explanation**: Multiplies `duration_seconds` by 2, storing the result in `doubled_duration`.

**Output**:

| EVENT\_ID | DOUBLED\_DURATION |
| --------- | ----------------- |
| 101       | 3.0               |
| 102       | 1.6               |

### Example 14: Using mathematical functions (divide)

**Goal**: Perform division on numerical values.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter duration_in_minutes = divide(duration_seconds, 60)
| fields event_id, duration_in_minutes
```

**Explanation**: Converts `duration_seconds` to minutes by dividing by 60, storing the result in `duration_in_minutes`.

**Output**:

| EVENT\_ID | DURATION\_IN\_MINUTES |
| --------- | --------------------- |
| 101       | 0.025                 |
| 102       | 0.0133                |

### Example 15: Using array functions (arraycreate)

**Goal**: Form a new array from specified values.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter default_tags = arraycreate("default_tag", "processed")
| fields event_id, default_tags
```

**Explanation**: Creates a new array `default_tags` containing the specified string values for each record.

**Output**:

| EVENT\_ID | DEFAULT\_TAGS                  |
| --------- | ------------------------------ |
| 101       | \["default\_tag", "processed"] |
| 102       | \["default\_tag", "processed"] |

### Example 16: Using array functions (arraymap)

**Goal**: Apply a function to each element of an array.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter positive_codes = arraymap(numeric_codes, if("@element" < 0, 0, "@element"))
| fields event_id, positive_codes
```

**Explanation**: Creates `positive_codes` by going through the array `numeric_codes` and replacing any negative values with 0.

**Output**:

| EVENT\_ID | POSITIVE\_CODES     |
| --------- | ------------------- |
| 101       | \[13, 0, 29, 82, 0] |
| 102       | \[0, 56, 13, 0, 42] |

### Example 17: Using array functions (arrayrange)

**Goal**: Generate a portion of an array based on specified indices.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter first_two_tags = arrayrange(string_tags, 0, 2)
| fields event_id, first_two_tags
```

**Explanation**: Extracts the first two elements (indices 0 and 1) from the `string_tags` array into `first_two_tags`.

**Output**:

| EVENT\_ID | FIRST\_TWO\_TAGS            |
| --------- | --------------------------- |
| 101       | \["security", "login"]      |
| 102       | \["filesystem", "critical"] |

## Related articles

* **Stages**: [`filter`](filter), [`fields`](fields)
* **Functions**: [`concat`](../functions/concat), [`lowercase`](../functions/lowercase), [`split`](../functions/split), [`json_extract_scalar`](../functions/json_extract_scalar), [`json_extract_array`](../functions/json_extract_array), [`if`](../functions/if), [`coalesce`](../functions/coalesce), [`format_timestamp`](../functions/format_timestamp), [`add`](../functions/add), [`multiply`](../functions/multiply), [`divide`](../functions/divide), [`arraycreate`](../functions/arraycreate), [`arraymap`](../functions/arraymap), [`arrayrange`](../functions/arrayrange)
