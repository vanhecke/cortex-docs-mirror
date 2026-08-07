# replex

Use the `replex()` function to identify a substring (pattern) and replace it with a new string.

## Syntax

```sql
replex (<string>, <pattern>, <new_string>)
```

## Parameters

| Name         | Type   | Required | Description                                                                                                              |
| ------------ | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------ |
| `string`     | string | Yes      | The string field or literal value you want to modify.                                                                    |
| `pattern`    | string | Yes      | The regular expression pattern to find and replace. The pattern must be enclosed in double quotes.                       |
| `new_string` | string | Yes      | The string that will replace all occurrences of the matched pattern. This string must also be enclosed in double quotes. |

## Returns

The `replex()` function returns a new string with the replacements made. If the pattern is not found, the original string is returned unchanged.

## Usage notes

* The `replex()` function operates exclusively on string inputs.
* The function replaces **all** occurrences of the specified regular expression pattern within the input field.
* XQL uses the RE2 regular expression implementation.
* By default, regex patterns are case-sensitive. To achieve case-insensitive matching, the `(?i)` syntax should be added once at the beginning of the inline regular expression within the pattern string.
* The `replex()` function is typically used within the `alter` stage to create new fields or modify existing ones.

## Examples

### Example 1: Simple pattern replacement (masking a specific IP address)

**Goal**: Replace a specific IP address (`192.168.1.10`) in the `raw_log_data` field with a placeholder `INTERNAL_IP`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 101 
| alter masked_log = replex(raw_log_data, "192\.168\.1\.10", "INTERNAL_IP") 
| fields event_id, raw_log_data, masked_log 
```

**Explanation**: The query finds the literal IP "192.168.1.10" (escaped dots for regex literal match) in `raw_log_data` for `event_id` 101 and replaces it with "INTERNAL\_IP", creating the `masked_log` field.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                           | MASKED\_LOG                              |
| --------- | ---------------------------------------- | ---------------------------------------- |
| 101       | "User Alice logged in from 192.168.1.10" | "User Alice logged in from INTERNAL\_IP" |

### Example 2: Using regex character classes for general IP address masking

**Goal**: Use a regular expression to find and mask any standard IPv4 address pattern in the `raw_log_data` or `ipv4_address` fields.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id in (101, 103)
| alter masked_ipv4 = replex(ipv4_address, "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}", "MASKED_ADDR") 
| alter masked_raw_log = replex(raw_log_data, "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}", "MASKED_IP") 
| fields event_id, ipv4_address, masked_ipv4, raw_log_data, masked_raw_log 
```

**Explanation**: The query uses the regex `\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}` to identify and replace dotted-decimal IPv4 addresses. For event 101, `ipv4_address` is masked. For event 103, the IP in `raw_log_data` is masked.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS  | MASKED\_IPV4   | RAW\_LOG\_DATA                                         | MASKED\_RAW\_LOG                                          |
| --------- | -------------- | -------------- | ------------------------------------------------------ | --------------------------------------------------------- |
| 101       | "192.168.1.10" | "MASKED\_ADDR" | "User Alice logged in from 192.168.1.10"               | "User Alice logged in from MASKED\_IP"                    |
| 103       | NULL           | NULL           | "Outbound connection to 1.1.1.1:443 initiated by AppX" | "Outbound connection to MASKED\_IP:443 initiated by AppX" |

### Example 3: Replacing multiple occurrences of a word

**Goal**: Target `raw_log_data` and replace multiple instances of whitespace characters with "\_".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 103
| alter updated_log = replex(raw_log_data, "\s", "_") 
| fields event_id, raw_log_data, updated_log 
```

**Explanation**: The `replex()` function finds all instances of the whitespace character " " and replaces them with "\_".

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                         | UPDATED\_LOG                                                 |
| --------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| 103       | "Outbound connection to 1.1.1.1:443 initiated by AppX" | "Outbound\_connection\_to\_1.1.1.1:443\_initiated\_by\_AppX" |

### Example 4: Case-insensitive replacement using (?i)

**Goal**: Perform a case-insensitive replacement by using the `(?i)` flag to match "User" or "user" regardless of capitalization, replacing it with "ACCOUNT\_HOLDER" in `event_description`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw
| filter event_id = 101 
| alter anonymized_desc = replex(event_description, "(?i)user", "ACCOUNT_HOLDER") 
| fields event_id, event_description, anonymized_desc 
```

**Explanation**: By prefixing the regex with `(?i)`, `replex()` ignores case, successfully replacing "User" (with a capital 'U') in `event_description` with "ACCOUNT\_HOLDER".

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      | ANONYMIZED\_DESC                   |
| --------- | ----------------------- | ---------------------------------- |
| 101       | "User login successful" | "ACCOUNT\_HOLDER login successful" |

### Example 5: Removing a pattern (replacing with an empty string)

**Goal**: Remove the " from " followed by an IP address from `raw_log_data` by replacing the pattern with an empty string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter cleaned_log = replex(raw_log_data, " from \d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}", "") 
| fields event_id, raw_log_data, cleaned_log 
| filter event_id = 101 
```

**Explanation**: The regex matches " from " followed by any IPv4 pattern. `replex()` then replaces this entire matched substring with an empty string, effectively removing it and cleaning the `raw_log_data` entry.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                           | CLEANED\_LOG           |
| --------- | ---------------------------------------- | ---------------------- |
| 101       | "User Alice logged in from 192.168.1.10" | "User Alice logged in" |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`replace`](replace), [`regextract`](regextract), [`regexcapture`](regexcapture)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
