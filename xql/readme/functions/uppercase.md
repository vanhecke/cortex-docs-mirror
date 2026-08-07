# uppercase

Use the `uppercase()` function to convert all characters in a given string field value or literal to their uppercase equivalents.

## Syntax

```sql
uppercase (<string>)
```

## Parameters

| Name       | Type   | Required | Description                                                           |
| ---------- | ------ | -------- | --------------------------------------------------------------------- |
| `<string>` | string | Yes      | The input string field or literal value to be converted to uppercase. |

## Returns

The `uppercase()` function returns a string with all characters converted to uppercase.

## Usage notes

* The `uppercase()` function is typically used within the `alter` stage to create new fields or modify existing ones.
* The function can also be used in `filter` stages, particularly in scenarios where case-insensitive comparisons are needed or to align with `config case_sensitive = false` behavior.

## Examples

### Example 1: uppercase() on a direct string field

**Goal**: Convert the `event_description` field to all uppercase letters.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter upper_description = uppercase(event_description)
| fields event_id, event_description, upper_description
| limit 3
```

**Explanation**: The `uppercase()` function converts the text in the `event_description` field to its all-uppercase equivalent, creating a new field `upper_description`.

**Output**:

| event\_id | event\_description               | upper\_description               |
| --------- | -------------------------------- | -------------------------------- |
| 101       | "User login successful"          | "USER LOGIN SUCCESSFUL"          |
| 102       | "File access attempt"            | "FILE ACCESS ATTEMPT"            |
| 103       | "Network connection established" | "NETWORK CONNECTION ESTABLISHED" |

### Example 2: uppercase() on a string field (for example, Domain Name)

**Goal**: Standardize domain names in the `dst_domain` field to uppercase.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter upper_domain = uppercase(dst_domain)
| fields event_id, dst_domain, upper_domain
| limit 3
```

**Explanation**: The `uppercase()` function transforms the `dst_domain` strings, including any surrounding quotes, into their uppercase format in the `upper_domain` field.

**Output**:

| event\_id | dst\_domain         | upper\_domain       |
| --------- | ------------------- | ------------------- |
| 101       | "ec2.amazonaws.com" | "EC2.AMAZONAWS.COM" |
| 102       | "sts.amazonaws.com" | "STS.AMAZONAWS.COM" |
| 103       | "www.google.com"    | "WWW.GOOGLE.COM"    |

### Example 3: uppercase() used in conjunction with filter

**Goal**: Convert `raw_log_data` to uppercase and then use the result in a `filter` stage to find specific patterns regardless of original case.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter upper_log_data = uppercase(raw_log_data)
| filter upper_log_data contains "PROCESS"
| fields event_id, raw_log_data, upper_log_data
| limit 2
```

**Explanation**: The `raw_log_data` is converted to `upper_log_data`, which is then used in a `contains` filter. This effectively performs a case-insensitive search for "process" by first normalizing the case.

**Output**:

| event\_id | raw\_log\_data                                            | upper\_log\_data                                          |
| --------- | --------------------------------------------------------- | --------------------------------------------------------- |
| 102       | "Process cmd.exe attempted to access /etc/passwd"         | "PROCESS CMD.EXE ATTEMPTED TO ACCESS /ETC/PASSWD"         |
| 105       | "Transformed data from source X, processed 1000 records." | "TRANSFORMED DATA FROM SOURCE X, PROCESSED 1000 RECORDS." |

### Example 4: uppercase() on an extracted JSON string field

**Goal**: Extract a string value from a JSON field (`simple_json_data`) and apply `uppercase()` to it.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter json_status_string = simple_json_data -> status
| alter uppercase_json_status = uppercase(json_status_string)
| fields event_id, simple_json_data, json_status_string, uppercase_json_status
| limit 3
```

**Explanation**: The `status` field is extracted from `simple_json_data` as a string (`json_status_string`), and then `uppercase()` converts this extracted value to uppercase for the `uppercase_json_status` field. Events where the `status` field does not exist will result in `NULL`.

**Output**:

| event\_id | simple\_json\_data                                | json\_status\_string | uppercase\_json\_status |
| --------- | ------------------------------------------------- | -------------------- | ----------------------- |
| 101       | {"status": "ok", "code": 200}                     | "ok"                 | "OK"                    |
| 102       | {"status": "fail", "error": "access\_denied"}     | "fail"               | "FAIL"                  |
| 103       | {"connection\_id": "CONN-001", "protocol": "TCP"} | NULL                 | NULL                    |

### Example 5: uppercase() within arraymap() for an array of Strings

**Goal**: Convert every element within the `string_tags` array to uppercase using `arraymap()`.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter uppercase_tags = arraymap(string_tags, uppercase("@element"))
| fields event_id, string_tags, uppercase_tags
| limit 3
```

**Explanation**: The `arraymap()` function iterates through each element (`@element`) of the `string_tags` array, applying the `uppercase()` function to each one. The result is a new array, `uppercase_tags`, where all original elements are now in uppercase.

**Output**:

| event\_id | string\_tags                | uppercase\_tags             |
| --------- | --------------------------- | --------------------------- |
| 101       | \["security", "login"]      | \["SECURITY", "LOGIN"]      |
| 102       | \["filesystem", "critical"] | \["FILESYSTEM", "CRITICAL"] |
| 103       | \["network", "cloud"]       | \["NETWORK", "CLOUD"]       |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`config`](../stages/config), [`limit`](../stages/limit)
* **Functions**: [`arraymap`](arraymap), [`lowercase`](lowercase)
