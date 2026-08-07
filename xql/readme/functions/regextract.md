# regextract

Use the `regextract()` function to extract a substring from a field value using a regular expression pattern. The function returns the first captured group from the regex match. This is a scalar function used within the `alter` stage.

## Syntax

```sql
| alter <output_field> = regextract(<field>, "<regex_pattern>")
```

## Parameters

| Name            | Type           | Required | Description                                                                                                                             |
| --------------- | -------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `field`         | string         | Yes      | The string field from which to extract a substring.                                                                                     |
| `regex_pattern` | string (regex) | Yes      | A regular expression pattern with at least one capture group `()`. The function returns the content matched by the first capture group. |

## Returns

**Type**: string

**Description**: The `regextract()` function returns the substring matched by the first capture group in the regular expression. Returns NULL if the pattern does not match the input string or if the input field is NULL.

## Usage notes

* **Capture groups**: The regex pattern must contain at least one capture group defined by parentheses `()`. Only the first capture group is returned.
* **No match**: If the regex does not match the input string, the function returns NULL.
* **Case sensitivity**: Regular expression matching is case-sensitive by default.
* **Escape characters**: Special regex characters must be escaped with a backslash `\` (for example, `\.` to match a literal dot).
* **Scalar function**: `regextract()` is a scalar function used in the `alter` stage, not an aggregation function. The function operates on each row individually.
* **Multiple extractions**: To extract multiple parts from a string, use multiple `alter` statements with different capture groups.

## Examples

### Example 1: Extract domain from email address

**Goal**: Extract the domain portion from an email address field.

**XQL code**:

```sql
dataset = xdr_data
| alter domain = regextract(actor_effective_username, "@(.+)$")
```

**Explanation**: The regex `@(.+)$` matches the `@` symbol followed by one or more characters until the end of the string. The capture group `(.+)` captures the domain portion.

**Output**:

| ACTOR\_EFFECTIVE\_USERNAME | DOMAIN       |
| -------------------------- | ------------ |
| admin@example.com          | example.com  |
| user1@corp.local           | corp.local   |
| svc\_account@internal.net  | internal.net |

### Example 2: Extract IP address from a log message

**Goal**: Extract an IPv4 address from a free-text log message.

**XQL code**:

```sql
dataset = xdr_data
| alter extracted_ip = regextract(action_file_path, "(\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})")
```

**Explanation**: The regex pattern `(\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})` matches an IPv4 address pattern. The entire match is captured by the outer parentheses.

**Output**:

| ACTION\_FILE\_PATH                        | EXTRACTED\_IP |
| ----------------------------------------- | ------------- |
| Connection from 192.168.1.100 on port 443 | 192.168.1.100 |
| Failed login attempt from 10.0.0.5        | 10.0.0.5      |
| No IP in this entry                       | null          |

### Example 3: Extract file extension from file path

**Goal**: Extract the file extension from a file path.

**XQL code**:

```sql
dataset = xdr_data
| alter file_ext = regextract(action_file_path, "\.([^.]+)$")
```

**Explanation**: The regex `\.([^.]+)$` matches a literal dot followed by one or more non-dot characters at the end of the string. The capture group `([^.]+)` captures the file extension without the dot.

**Output**:

| ACTION\_FILE\_PATH          | FILE\_EXT |
| --------------------------- | --------- |
| C:\Windows\System32\cmd.exe | exe       |
| /var/log/syslog.log         | log       |
| /tmp/archive.tar.gz         | gz        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields)
* **Functions**: `regextract_all()`, [`replace()`](replace), `contains()`
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
