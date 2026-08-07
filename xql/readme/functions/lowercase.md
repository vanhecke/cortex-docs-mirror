# lowercase

Use the `lowercase()` function to convert all characters in a specified string field or literal to their corresponding lowercase representation.

## Syntax

```sql
lowercase (<string>)
```

## Parameters

| Name     | Type   | Required | Description                                                           |
| -------- | ------ | -------- | --------------------------------------------------------------------- |
| `string` | string | Yes      | The input string field or literal value to be converted to lowercase. |

## Returns

The `lowercase()` function returns a string where all characters of the input have been converted to lowercase.

## Usage notes

* The function requires a string input.
* If a `NULL` value is passed to the function, it returns `NULL`.
* This function is typically used within the `alter` stage to create new fields or modify existing ones.
* The function can also be directly used within `filter` stages to enable case-insensitive comparisons without setting `config case_sensitive = false` globally.

## Examples

### Example 1: Lowercasing an existing string field

**Goal**: Convert the `event_description` field to all lowercase letters.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter lower_description = lowercase(event_description)
| fields event_id, event_description, lower_description
| limit 3
```

**Explanation**: This query creates a new field, `lower_description`, containing the lowercase version of each `event_description`.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | LOWER\_DESCRIPTION               |
| --------- | -------------------------------- | -------------------------------- |
| 101       | "User login successful"          | "user login successful"          |
| 102       | "File access attempt"            | "file access attempt"            |
| 103       | "Network connection established" | "network connection established" |

### Example 2: Lowercasing a literal string

**Goal**: Convert a direct string literal with mixed case to lowercase.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter lower_literal = lowercase("PaLo AlTo NeTwOrKs")
| fields event_id, lower_literal
| limit 3
```

**Explanation**: This query adds a new field, `lower_literal`, which contains the constant lowercase string "palo alto networks" for each record.

**Output**:

| EVENT\_ID | LOWER\_LITERAL       |
| --------- | -------------------- |
| 101       | "palo alto networks" |
| 102       | "palo alto networks" |
| 103       | "palo alto networks" |

### Example 3: Lowercasing a string extracted from JSON data

**Goal**: Extract a string value from a JSON field and convert it to lowercase.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter status_string = simple_json_data -> status
| alter lower_json_status = lowercase(status_string)
| fields event_id, simple_json_data, status_string, lower_json_status
| limit 3
```

**Explanation**: This query extracts the `status` value from `simple_json_data` as a string and then converts it to lowercase. For `event_id` 103, because `simple_json_data` does not contain a `status` key, `status_string` becomes `NULL`, and subsequently, `lower_json_status` also becomes `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | STATUS\_STRING | LOWER\_JSON\_STATUS |
| --------- | ------------------------------------------------- | -------------- | ------------------- |
| 101       | {"status": "ok", "code": 200}                     | "ok"           | "ok"                |
| 102       | {"status": "fail", "error": "access\_denied"}     | "fail"         | "fail"              |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL           | NULL                |

### Example 4: Lowercasing a numerical field after explicit string conversion

**Goal**: Convert a numerical field to a string and then attempt to lowercase it.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_string = to_string(event_id)
| alter lower_id_string = lowercase(event_id_string)
| fields event_id, event_id_string, lower_id_string
| limit 3
```

**Explanation**: This query first converts the numerical `event_id` to its string representation (for example, 101 becomes "101") and then attempts to lowercase it. Because numeric strings only contain digits, the `lowercase()` function does not alter them.

**Output**:

| EVENT\_ID | EVENT\_ID\_STRING | LOWER\_ID\_STRING |
| --------- | ----------------- | ----------------- |
| 101       | "101"             | "101"             |
| 102       | "102"             | "102"             |
| 103       | "103"             | "103"             |

### Example 5: Using lowercase() within a filter stage for case-insensitive matching

**Goal**: Filter for events containing a specific word, ignoring case sensitivity.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter lowercase(event_description) contains "user"
| fields event_id, event_description
| limit 3
```

**Explanation**: This query applies `lowercase()` to the `event_description` field for each record and then checks if the resulting lowercase string contains the substring "user". This allows it to match "User login successful" even though the original string has an uppercase 'U'.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      |
| --------- | ----------------------- |
| 101       | "User login successful" |

### Example: Normalize and deduplicate process names

**Goal**: Convert all `actor_process_image_name` field values that are not null to lowercase and return a list of unique values.

**XQL Code**:

```sql
dataset = ample_xql_raw 
| fields actor_process_image_name as apin 
| dedup apin by asc _time 
| filter apin != null 
| alter apin = lowercase(apin)
```

**Explanation**: The query begins by selecting the `actor_process_image_name` field from the `xample_xql_raw` dataset and aliasing it as `apin`.

* The `dedup` stage is used to keep only unique occurrences of each process name, specifically retaining the first occurrence based on ascending time.
* The `filter` stage removes any records where the process name is null.
* Finally, the `alter` stage applies the `lowercase()` function to the `apin` field, standardizing all unique process names into lowercase format for consistent reporting and analysis.

**Output**:

| apin        |
| ----------- |
| chrome.exe  |
| svchost.exe |
| terminal    |
| notepad.exe |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`uppercase`](uppercase), [`to_string`](to_string), [`json_extract_scalar`](json_extract_scalar)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
