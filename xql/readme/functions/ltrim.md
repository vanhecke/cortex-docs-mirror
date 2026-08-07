# ltrim

Use the `ltrim()` function to remove specified characters or whitespace from the beginning (left side) of a string.

## Syntax

```sql
ltrim (<string>, [trim_characters])
```

## Parameters

| Name              | Type   | Required | Description                                                                                                                                            |
| ----------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `string`          | string | Yes      | The string field or literal value you wish to modify.                                                                                                  |
| `trim_characters` | string | No       | A string containing the set of characters to remove from the left side of the string. If omitted, defaults to whitespace characters (spaces and tabs). |

## Returns

The `ltrim()` function returns a new string with the specified leading characters removed.

## Usage notes

* The `trim_characters` parameter is treated as a **set** of individual characters. Any character from this set found at the beginning of the string will be removed repeatedly until a character that is not in the set is encountered.
* If the `trim_characters` parameter is not specified, the function defaults to removing leading whitespace characters (spaces and tabs).
* If a `NULL` value is passed as the input string, the function returns `NULL`.

## Examples

### Example 1: Removing leading whitespace (default behavior)

**Goal**: Remove leading spaces from a literal string by relying on the function's default behavior.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter trimmed_text = ltrim("   Important Message") 
| fields event_id, trimmed_text 
| limit 3
```

**Explanation**: This query creates a new field, `trimmed_text`, where the leading spaces from the literal string " Important Message" are removed, resulting in "Important Message".

**Output**:

| EVENT\_ID | TRIMMED\_TEXT     |
| --------- | ----------------- |
| 101       | Important Message |
| 102       | Important Message |
| 103       | Important Message |

### Example 2: Removing a specific exact prefix

**Goal**: Remove the exact "www." prefix from the `dst_domain` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter trimmed_domain = ltrim(dst_domain, "www.") 
| fields event_id, dst_domain, trimmed_domain 
| limit 3
```

**Explanation**: For `event_id` 103, the leading "www." from "www.google.com" is removed, leaving "google.com". For other records where the `trim_characters` ("www.") are not found at the very beginning, the string remains unchanged.

**Output**:

| EVENT\_ID | DST\_DOMAIN       | TRIMMED\_DOMAIN   |
| --------- | ----------------- | ----------------- |
| 101       | ec2.amazonaws.com | ec2.amazonaws.com |
| 102       | sts.amazonaws.com | sts.amazonaws.com |
| 103       | www.google.com    | google.com        |

### Example 3: Removing specific leading characters (character set removal)

**Goal**: Remove a set of characters ('U', 'e', 'o', 'r', space) from the beginning of the `raw_log_data` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter processed_log = ltrim(raw_log_data, "Ueor ") 
| fields event_id, raw_log_data, processed_log 
| limit 3
```

**Explanation**: For `event_id` 101, the log starts with "User Alice...". 'U' is in the set "Ueor ", so it is removed. The next character 's' is _not_ in the set, so the process stops. The result is "ser Alice logged in from 192.168.1.10".

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                       | PROCESSED\_LOG                                       |
| --------- | ---------------------------------------------------- | ---------------------------------------------------- |
| 101       | User Alice logged in from 192.168.1.10               | ser Alice logged in from 192.168.1.10                |
| 102       | Process cmd.exe attempted to access /etc/passwd      | Process cmd.exe attempted to access /etc/passwd      |
| 103       | Outbound connection to 1.1.1.1:443 initiated by AppX | Outbound connection to 1.1.1.1:443 initiated by AppX |

### Example 4: ltrim() on a string extracted from JSON data

**Goal**: Remove specific characters ('f' or 'o') from the beginning of a string extracted from a JSON field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter status_string = simple_json_data -> status 
| alter trimmed_json_status = ltrim(status_string, "fo") 
| fields event_id, simple_json_data, status_string, trimmed_json_status 
| limit 3
```

**Explanation**: For `event_id` 101, "ok" becomes "k" because 'o' is removed. For `event_id` 102, "fail" becomes "ail" because 'f' is removed. For `event_id` 103, `status_string` is `NULL`, so `trimmed_json_status` is also `NULL`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                                | STATUS\_STRING | TRIMMED\_JSON\_STATUS |
| --------- | ------------------------------------------------- | -------------- | --------------------- |
| 101       | {"status": "ok", "code": 200}                     | ok             | k                     |
| 102       | {"status": "fail", "error": "access\_denied"}     | fail           | ail                   |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL           | NULL                  |

### Example 5: ltrim() on a numerical field after explicit string conversion

**Goal**: Remove specific digits ('1' or '0') from the beginning of the `event_id` field after converting it to a string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_id_string = to_string(event_id) 
| alter trimmed_id_string = ltrim(event_id_string, "10") 
| fields event_id, event_id_string, trimmed_id_string 
| limit 3
```

**Explanation**: For `event_id` 101 ("101"), '1', then '0', then '1' are all removed because they are in the set "10", resulting in an empty string. For `event_id` 102 ("102"), '1' and '0' are removed, leaving "2". For `event_id` 103 ("103"), '1' and '0' are removed, leaving "3".

**Output**:

| EVENT\_ID | EVENT\_ID\_STRING | TRIMMED\_ID\_STRING |
| --------- | ----------------- | ------------------- |
| 101       | 101               |                     |
| 102       | 102               | 2                   |
| 103       | 103               | 3                   |

### Example 6: ltrim() on a field with no matching leading characters

**Goal**: Attempt to remove characters ('x', 'y', 'z') that do not exist at the start of the string field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter no_change_desc = ltrim(event_description, "xyz") 
| fields event_id, event_description, no_change_desc 
| limit 3
```

**Explanation**: Because none of the characters 'x', 'y', or 'z' are present at the beginning of "User login successful" or other `event_description` values, the function returns the original string unchanged.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             | NO\_CHANGE\_DESC               |
| --------- | ------------------------------ | ------------------------------ |
| 101       | User login successful          | User login successful          |
| 102       | File access attempt            | File access attempt            |
| 103       | Network connection established | Network connection established |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields)
* **Functions**: [`rtrim`](rtrim), [`trim`](trim), [`to_string`](to_string), [`json_extract_scalar`](json_extract_scalar)
