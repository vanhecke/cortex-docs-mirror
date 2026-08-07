# wildcard\_match

Use the `wildcard_match` function to determine if a given string matches a specified wildcard pattern. The function is primarily used for flexible pattern matching beyond literal equality, often for filtering or categorizing data.

## Syntax

```sql
wildcard_match(<string_value>, <wildcard_pattern>)
```

## Parameters

| Name               | Type   | Required | Description                                                                  |
| ------------------ | ------ | -------- | ---------------------------------------------------------------------------- |
| `string_value`     | string | Yes      | The input string field or literal value to be evaluated against the pattern. |
| `wildcard_pattern` | string | Yes      | The pattern string, which can include wildcard characters `*` and `?`.       |

## Returns

The function returns a boolean value: `true` if the string matches the pattern, and `false` otherwise.

## Usage notes

* **Availability**: This function is only available with Cortex XSIAM licenses that include Cortex Cloud.
* **Wildcard characters**:
* `*` (Asterisk): Matches a sequence of zero or more (possibly different) characters.
* `?` (Question Mark): Matches exactly one character.
* **Case sensitivity**: By default, the function is case-sensitive. To perform a case-insensitive match, you must add the `(?i)` syntax once at the beginning of the regular expression within the pattern string.
* **Stage usage**: This function is typically used within the `alter` stage to create new boolean fields or directly within `filter` stages to narrow down results.

## Examples

### Example 1: Basic wildcard matching with `*`

**Goal**: Check if the `event_description` starts with "User" and ends with "successful".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter matches_user_login = wildcard_match(event_description, "User*successful") 
| fields event_id, event_description, matches_user_login 
| limit 2 

```

**Explanation**: The function returns `true` for event 101 because "User login successful" matches the pattern "User\*successful". The query returns `false` for event 102 because "File access attempt" does not match.

**Output:**

| event\_id | event\_description      | matches\_user\_login |
| --------- | ----------------------- | -------------------- |
| 101       | "User login successful" | true                 |
| 102       | "File access attempt"   | false                |

### Example 2: Wildcard matching with `?`

**Goal**: Use the `?` wildcard to match exactly one character within the `raw_log_data` field, targeting a specific process name pattern like "c?d.exe".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter matches_cmd_pattern = wildcard_match(raw_log_data, "Process c?d.exe*") 
| fields event_id, raw_log_data, matches_cmd_pattern 
| limit 2 

```

**Explanation**: For event 102, the string "Process cmd.exe..." matches the pattern because the 'm' in "cmd" is a single character matched by `?`. Event 101 does not match the pattern.

**Output:**

| event\_id | raw\_log\_data                                    | matches\_cmd\_pattern |
| --------- | ------------------------------------------------- | --------------------- |
| 101       | "User Alice logged in from 192.168.1.10"          | false                 |
| 102       | "Process cmd.exe attempted to access /etc/passwd" | true                  |

### Example 3: Complex pattern with `*` and `?`

**Goal**: Combine both wildcards to match a complex file path pattern in `raw_log_data`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter matches_complex_pattern = wildcard_match(raw_log_data, "*cmd.ex? attempted to access /*/passw?d") 
| fields event_id, raw_log_data, matches_complex_pattern 
| limit 2 

```

**Explanation**: The pattern uses `*` to match variable segments ("Process " and "tc/") and `?` to match specific single characters ('e' in exe and 'd' in passwd). This correctly identifies event 102 as a match.

**Output:**

| event\_id | raw\_log\_data                                    | matches\_complex\_pattern |
| --------- | ------------------------------------------------- | ------------------------- |
| 101       | "User Alice logged in from 192.168.1.10"          | false                     |
| 102       | "Process cmd.exe attempted to access /etc/passwd" | true                      |

### Example 4: Case-insensitive matching

**Goal**: Perform a case-insensitive check on `event_description` using the `(?i)` flag.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter matches_case_insensitive = wildcard_match(event_description, "(?i)user*login*successful") 
| fields event_id, event_description, matches_case_insensitive 
| limit 2 

```

**Explanation**: Even though `event_description` starts with an uppercase "User" and the pattern specifies "user", the `(?i)` flag enables case-insensitive matching, resulting in `true` for event 101.

**Output:**

| event\_id | event\_description      | matches\_case\_insensitive |
| --------- | ----------------------- | -------------------------- |
| 101       | "User login successful" | true                       |
| 102       | "File access attempt"   | false                      |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`replex`](replex), [`replace`](replace)
