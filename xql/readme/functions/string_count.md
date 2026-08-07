# string\_count

Use the `string_count()` function to count the number of times a specified substring (pattern) appears within a given string.

## Syntax

```sql
string_count (<string>, <pattern>)
```

## Parameters

| Name      | Type   | Required | Description                                                          |
| --------- | ------ | -------- | -------------------------------------------------------------------- |
| `string`  | string | Yes      | The input string field or literal value in which you want to search. |
| `pattern` | string | Yes      | The substring literal that you want to count.                        |

## Returns

The `string_count()` function returns an integer representing the number of occurrences found.

## Usage notes

* By default, XQL queries operate with case-sensitivity unless `config case_sensitive = false` is explicitly set. This also applies to `string_count()`.
* If the input `string` value is `NULL`, the `string_count()` function will return `NULL`.
* If the `pattern` does not appear in the `string`, the function returns `0`.

## Examples

### Example 1: Counting occurrences of a specific character in a string field

**Goal**: Count the occurrences of the character 'o' in the `event_description` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id in (101, 102, 103) // Focus on relevant records from sample_xql_raw
| alter count_of_o = string_count(event_description, "o") // Counts occurrences of 'o' 
| fields event_id, event_description, count_of_o 
```

**Explanation**: The query counts how many times the character 'o' appears in the `event_description` for each specified event.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | COUNT\_OF\_O |
| --------- | -------------------------------- | ------------ |
| 101       | "User login successful"          | 1            |
| 102       | "File access attempt"            | 0            |
| 103       | "Network connection established" | 3            |

### Example 2: Counting occurrences of a substring (word) in a string field

**Goal**: Count the occurrences of the word "access" in the `raw_log_data` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id in (101, 102) // Focus on relevant records
| alter count_of_access = string_count(raw_log_data, "access") // Counts occurrences of 'access' 
| fields event_id, raw_log_data, count_of_access 
```

**Explanation**: The `string_count()` function correctly identifies and counts the single occurrence of "access" in event ID 102's `raw_log_data`.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                    | COUNT\_OF\_ACCESS |
| --------- | ------------------------------------------------- | ----------------- |
| 101       | "User Alice logged in from 192.168.1.10"          | 0                 |
| 102       | "Process cmd.exe attempted to access /etc/passwd" | 1                 |

### Example 3: Counting delimiters in an IP address string

**Goal**: Count the number of dot (`.`) delimiters within `ipv4_address` strings.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id in (101, 102) // Focus on relevant records
| alter count_of_dots = string_count(ipv4_address, ".") // Counts occurrences of '.' 
| fields event_id, ipv4_address, count_of_dots 
```

**Explanation**: The query accurately counts the three dot separators in each IPv4 address string.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS  | COUNT\_OF\_DOTS |
| --------- | -------------- | --------------- |
| 101       | "192.168.1.10" | 3               |
| 102       | "10.0.0.5"     | 3               |

### Example 4: Case-insensitive counting (default behavior)

**Goal**: Demonstrate `string_count()`'s default case-sensitive behavior by searching for "user" (lowercase) in a field containing "User" (uppercase).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 101 // Focus on a single record
| alter count_user_lowercase_search = string_count(raw_log_data, "user") // Searches for 'user' 
| fields event_id, raw_log_data, count_user_lowercase_search 
```

**Explanation**: The pattern "user" (lowercase) does not successfully match "User" in the `raw_log_data` due to the case-sensitive behavior of XQL.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                           | COUNT\_USER\_LOWERCASE\_SEARCH |
| --------- | ---------------------------------------- | ------------------------------ |
| 101       | "User Alice logged in from 192.168.1.10" | 0                              |

### Example 5: Case-sensitive counting (with `config case_sensitive = false`)

**Goal**: Explicitly set case sensitivity to `false` to show how it affects `string_count()` results when searching for "user" vs. "User".

**XQL code**:

```sql
config case_sensitive = false // Explicitly enable case in-sensitivity 
| dataset = sample_xql_raw
| filter event_id = 101 // Focus on a single record
| alter count_User_uppercase_search = string_count(raw_log_data, "User") // Searches for 'User' 
| alter count_user_lowercase_search = string_count(raw_log_data, "user") // Searches for 'user' 
| fields event_id, raw_log_data, count_User_uppercase_search, count_user_lowercase_search 
```

**Explanation**: When `config case_sensitive` is `false`, `string_count()` does not distinguish between "User" and "user", returning `1` for both cases.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                           | COUNT\_USER\_UPPERCASE\_SEARCH | COUNT\_USER\_LOWERCASE\_SEARCH |
| --------- | ---------------------------------------- | ------------------------------ | ------------------------------ |
| 101       | "User Alice logged in from 192.168.1.10" | 1                              | 1                              |

### Example 6: Counting a pattern not present in the string

**Goal**: Demonstrate the result when the specified pattern does not exist in the input string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 101 // Focus on a single record
| alter count_of_nonexistent_pattern = string_count(event_description, "nonexistent_word") // Searches for a non-existent word 
| fields event_id, event_description, count_of_nonexistent_pattern 
```

**Explanation**: As expected, `string_count()` returns `0` when the `nonexistent_word` pattern is not found in the `event_description`.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      | COUNT\_OF\_NONEXISTENT\_PATTERN |
| --------- | ----------------------- | ------------------------------- |
| 101       | "User login successful" | 0                               |

### Example 7: Handling `NULL` input string

**Goal**: Show how `string_count()` behaves when the input string field contains a `NULL` value.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter count_in_null_domain = string_count(dst_domain, ".") // Attempts to count in a NULL domain 
| fields event_id, dst_domain, count_in_null_domain 
| filter event_id = 105 // Focus on record with NULL dst_domain 
```

**Explanation**: Consistent with XQL function behavior, if the input string (`dst_domain` for event ID 105) is `NULL`, the `string_count()` function returns `NULL`.

**Output**:

| EVENT\_ID | DST\_DOMAIN | COUNT\_IN\_NULL\_DOMAIN |
| --------- | ----------- | ----------------------- |
| 105       | NULL        | NULL                    |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`config`](../stages/config)
* **Functions**: [`len`](len), [`split`](split), [`regextract`](regextract)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
