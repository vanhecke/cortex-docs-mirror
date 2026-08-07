# rtrim

Use the `rtrim()` function to remove specific characters or whitespace from the end (right side) of a given string.

## Syntax

```sql
rtrim (<string>,[trim_characters])
```

## Parameters

| Name              | Type   | Required | Description                                                                                                                                                  |
| ----------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `string`          | string | Yes      | The string field or literal value from which you want to remove characters.                                                                                  |
| `trim_characters` | string | No       | A string containing the characters to be removed from the end of the input string. If this parameter is omitted, trailing whitespace characters are removed. |

## Returns

The `rtrim` function returns a new string with the specified characters removed from its end. If no matching characters are found at the end, the original string is returned unchanged.

## Usage notes

* The function operates exclusively on string inputs.
* The function removes all occurrences of any character found within the `trim_characters` set, starting from the rightmost character of the input string and continuing until a character not in the `trim_characters` set is encountered.
* The `trim_characters` specified in the pattern are case-sensitive.
* The function is typically used within the `alter` stage to create new fields or modify existing ones.

## Examples

### Example 1: Basic removal of a common suffix (from `dst_domain`)

**Goal**: Remove the ".com" suffix from domain names found in the `dst_domain` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id in (103, 104, 110)
| alter cleaned_domain = rtrim(dst_domain, ".com") 
| fields event_id, dst_domain, cleaned_domain 
```

**Explanation**: The `rtrim()` function successfully identifies and removes the ".com" suffix from the `dst_domain` values, creating the `cleaned_domain` field.

**Output**:

| EVENT\_ID | DST\_DOMAIN       | CLEANED\_DOMAIN |
| --------- | ----------------- | --------------- |
| 103       | "www.google.com"  | "www.google"    |
| 104       | "dropbox.com"     | "dropbox"       |
| 110       | "www.mongodb.com" | "www.mongodb"   |

### Example 2: Removing trailing whitespace (default behavior)

**Goal**: Use a literal string with trailing spaces to demonstrate `rtrim()`'s default behavior when no `trim_characters` are specified.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter raw_string_with_spaces = "User access login    " // Literal string with trailing spaces 
| alter trimmed_string = rtrim(raw_string_with_spaces) // Removes trailing whitespace by default 
| fields event_id, raw_string_with_spaces, trimmed_string 
| limit 1 // Limit output for brevity 
```

**Explanation**: By omitting the `trim_characters` argument, `rtrim()` automatically removes all trailing space characters from `raw_string_with_spaces`, resulting in `trimmed_string`.

**Output**:

| EVENT\_ID | RAW\_STRING\_WITH\_SPACES | TRIMMED\_STRING     |
| --------- | ------------------------- | ------------------- |
| 101       | "User access login "      | "User access login" |

### Example 3: Removing specific characters that repeat at the end

**Goal**: Remove multiple identical characters from the end of a string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter raw_string = "Report_final_v2.docx" // Literal string with a suffix 
| alter trimmed_string = rtrim(raw_string, "xcd.o") // Removes any of 'x', 'c', 'd', '.', 'o' from the end 
| fields event_id, raw_string, trimmed_string 
| limit 1 // Limit output for brevity 
```

**Explanation**: The `rtrim()` function removes 'x', 'c', 'd', '.', and 'o' from the end of `raw_string`. Because 'x' and 'c' are found at the very end, and then 'o', and then '.' and 'd', they are all removed, demonstrating `rtrim()`'s behavior with multiple matching trailing characters.

**Output**:

| EVENT\_ID | RAW\_STRING              | TRIMMED\_STRING     |
| --------- | ------------------------ | ------------------- |
| 101       | "Report\_final\_v2.docx" | "Report\_final\_v2" |

### Example 4: Characters to remove not present at the end

**Goal**: Illustrate that `rtrim()` only operates on the end of the string. If the `trim_characters` are present elsewhere but not at the very end, the string remains unchanged.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 102 // Focus on relevant record
| alter unchanged_log = rtrim(raw_log_data, ".exe") // Attempts to remove ".exe" 
| fields event_id, raw_log_data, unchanged_log 
```

**Explanation**: Although ".exe" is present in the `raw_log_data` for event 102, it is in the middle of the string, not at the end. As `rtrim()` only processes characters from the right, the string remains `unchanged_log`.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                    | UNCHANGED\_LOG                                    |
| --------- | ------------------------------------------------- | ------------------------------------------------- |
| 102       | "Process cmd.exe attempted to access /etc/passwd" | "Process cmd.exe attempted to access /etc/passwd" |

### Example 5: Case-sensitive nature of `trim_characters`

**Goal**: Demonstrate that the `trim_characters` parameter is case-sensitive. Removing "COM" (uppercase) will not affect a string ending in ".com" (lowercase).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 103 // Focus on relevant record
| alter domain_case_insensitive_try = rtrim(dst_domain, "COM") // Attempts to remove "COM" (uppercase) 
| alter domain_case_sensitive_success = rtrim(dst_domain, "com") // Successfully removes "com" (lowercase) 
| fields event_id, dst_domain, domain_case_insensitive_try, domain_case_sensitive_success 
```

**Explanation**: `domain_case_insensitive_try` remains unchanged because "COM" (uppercase) does not match ".com" (lowercase) at the end of the string. `domain_case_sensitive_success` successfully removes "com" because the case matches.

**Output**:

| EVENT\_ID | DST\_DOMAIN      | DOMAIN\_CASE\_INSENSITIVE\_TRY | DOMAIN\_CASE\_SENSITIVE\_SUCCESS |
| --------- | ---------------- | ------------------------------ | -------------------------------- |
| 103       | "www.google.com" | "www.google.com"               | "www.google."                    |

### Example 6: Trimming a string derived from a JSON field

**Goal**: Extract a string value from a JSON field and then apply `rtrim()` to it.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 101 // Focus on relevant record
| alter status_from_json = simple_json_data -> status) // Extracts "ok" for event 101 
| alter trimmed_status = rtrim(status_from_json, "k") // Removes 'k' 
| fields event_id, simple_json_data, status_from_json, trimmed_status 
```

**Explanation**: The `status_from_json` field is created by extracting the string "ok" from the `simple_json_data`. `rtrim()` then removes the 'k' character from the end of "ok", resulting in "o".

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA               | STATUS\_FROM\_JSON | TRIMMED\_STATUS |
| --------- | -------------------------------- | ------------------ | --------------- |
| 101       | "{"status": "ok", "code": 200} " | "ok"               | "o"             |

### Example 7: Trimming from an array element converted to string

**Goal**: Extract an element from an array field, convert it to a string, and then apply `rtrim()`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 104 // Focus on relevant record
| alter first_tag_string = arrayindex(string_tags, 0) // Extracts "monitoring" for event 104 
| alter trimmed_tag = rtrim(first_tag_string, "g") // Removes 'g' 
| fields event_id, string_tags, first_tag_string, trimmed_tag 
```

**Explanation**: The `first_tag_string` field captures the first element of `string_tags` (which is "monitoring" for event 104). `rtrim()` then removes the character 'g' from the end of "monitoring", resulting in "monitorin".

**Output**:

| EVENT\_ID | STRING\_TAGS       | FIRST\_TAG\_STRING | TRIMMED\_TAG |
| --------- | ------------------ | ------------------ | ------------ |
| 104       | "\["monitoring"] " | "monitoring"       | "monitorin"  |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`arrayindex`](arrayindex)
