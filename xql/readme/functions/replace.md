# replace

Use the `replace()` function to substitute all occurrences of a specified substring within a string field with a new replacement string.

## Syntax

```sql
replace (<field>, "<old_substring>", "<new_string>")
```

## Parameters

| Name            | Type   | Required | Description                                                                                                       |
| --------------- | ------ | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `field`         | string | Yes      | The string field or literal value you wish to modify.                                                             |
| `old_substring` | string | Yes      | The specific substring to be found and replaced. This must be enclosed in double quotes.                          |
| `new_string`    | string | Yes      | The string that will replace all occurrences of the `old_substring`. This must also be enclosed in double quotes. |

## Returns

The `replace()` function returns a new string with the replacements made. If the `old_substring` is not found, the original string is returned unchanged.

## Usage notes

* The `replace()` function operates exclusively on string inputs.
* The function replaces **all** occurrences of the specified `old_substring` within the input field.
* By default, `replace()` is case-sensitive. "user" will not replace "User" unless explicitly handled (for example, by combining with `lowercase()`).
* `replace()` is typically used within the `alter` stage to create new fields or modify existing ones.

## Examples

### Example 1: Simple replacement of a literal substring

**Goal**: Replace a specific word ("User") in `raw_log_data` with a new word ("Client").

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter raw_log_data contains "User" 
| alter modified_log = replace(raw_log_data, "User", "Client") 
| fields event_id, raw_log_data, modified_log 
```

**Explanation**: The query finds the literal string "User" in the `raw_log_data` for `event_id` 101 and replaces it with "Client", creating the `modified_log` field.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                           | MODIFIED\_LOG                              |
| --------- | ---------------------------------------- | ------------------------------------------ |
| 101       | "User Alice logged in from 192.168.1.10" | "Client Alice logged in from 192.168.1.10" |

### Example 2: Replacing with an empty string (removal)

**Goal**: Remove a specific phrase (" attempted to access") from `raw_log_data` by replacing it with an empty string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter raw_log_data contains "attempted to access"
| alter cleaned_log = replace(raw_log_data, " attempted to access", "") 
| fields event_id, raw_log_data, cleaned_log 
```

**Explanation**: The specified phrase is entirely removed from the `raw_log_data`, resulting in a more concise `cleaned_log`.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                    | CLEANED\_LOG                  |
| --------- | ------------------------------------------------- | ----------------------------- |
| 102       | "Process cmd.exe attempted to access /etc/passwd" | "Process cmd.exe /etc/passwd" |

### Example 3: Case-sensitive replacement

**Goal**: Demonstrate that `replace()` is case-sensitive by attempting to replace "user login" with "user logon" in `event_description` where "User login" is present.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_description contains "login"
| alter case_sensitive_change = replace(event_description, "user login", "user logon") 
| fields event_id, event_description, case_sensitive_change 
```

**Explanation**: Since `replace()` is case-sensitive, and "user login" (lowercase) does not exactly match "User login" (as it appears in "User login successful" which has an uppercase 'U'), no replacement occurs.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      | CASE\_SENSITIVE\_CHANGE |
| --------- | ----------------------- | ----------------------- |
| 101       | "User login successful" | "User login successful" |

### Example 4: Combining with lowercase() for case-insensitive replacement logic

**Goal**: Use `lowercase()` to standardize the input string before applying `replace()`, achieving a conceptual case-insensitive replacement.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_description contains "connection"
| alter lower_event_desc = lowercase(event_description) 
| alter case_insensitive_replace = replace(lower_event_desc, "network", "link") 
| fields event_id, event_description, lower_event_desc, case_insensitive_replace 
```

**Explanation**: By first converting `event_description` to lowercase, `replace()` successfully finds and replaces "network" with "link", demonstrating how to implement case-insensitive logic.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | LOWER\_EVENT\_DESC               | CASE\_INSENSITIVE\_REPLACE    |
| --------- | -------------------------------- | -------------------------------- | ----------------------------- |
| 103       | "Network connection established" | "network connection established" | "link connection established" |

### Example 5: Replacing a character with another character

**Goal**: Replace all spaces in `event_description` with underscores for a specific event.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 104 
| alter underscored_description = replace(event_description, " ", "_") 
| fields event_id, event_description, underscored_description 
```

**Explanation**: All spaces within the `event_description` are replaced by underscores.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION | UNDERSCORED\_DESCRIPTION |
| --------- | ------------------ | ------------------------ |
| 104       | "System heartbeat" | "System\_heartbeat"      |

### Example 6: Handling non-existent substrings

**Goal**: Demonstrate that if the `old_substring` is not found, the original string is returned unmodified.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 101 
| alter no_change_log = replace(raw_log_data, "NonExistentPhrase", "NewPhrase") 
| fields event_id, raw_log_data, no_change_log 
```

**Explanation**: Since "NonExistentPhrase" is not present in `raw_log_data`, the `no_change_log` field retains the original value of `raw_log_data`.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                           | NO\_CHANGE\_LOG                          |
| --------- | ---------------------------------------- | ---------------------------------------- |
| 101       | "User Alice logged in from 192.168.1.10" | "User Alice logged in from 192.168.1.10" |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`replex`](replex), [`lowercase`](lowercase), [`trim`](trim)
