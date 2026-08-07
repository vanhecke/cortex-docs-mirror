# if

Use the `if()` function to evaluate a boolean condition and return a specific value based on whether the result is true or false.

## Syntax

```sql
if (<boolean expression>, <true_return_expression>[, <false_return_expression>])
```

## Parameters

| Name                      | Type                            | Required | Description                                                                                               |
| ------------------------- | ------------------------------- | -------- | --------------------------------------------------------------------------------------------------------- |
| `boolean_expression`      | boolean                         | Yes      | The condition that the function evaluates to either true or false.                                        |
| `true_return_expression`  | string, integer, float, boolean | Yes      | The value returned if the boolean expression evaluates to true.                                           |
| `false_return_expression` | string, integer, float, boolean | No       | The value returned if the boolean expression evaluates to false. If omitted, the function returns `NULL`. |

## Returns

The `if()` function returns the value of the `true_return_expression` if the condition is met. If the condition is not met, it returns the `false_return_expression`, or `NULL` if the false return expression is not provided.

## Usage notes

* The first parameter must always be a boolean expression that evaluates to either true or false.
* If the `false_return_expression` is omitted and the boolean expression evaluates to false, the function returns `NULL`.
* It is a best practice for the `true_return_expression` and `false_return_expression` to return compatible data types (for example, both strings or both integers) to ensure predictable results.
* The function supports nested `if/else` logic, allowing you to chain multiple conditions sequentially.

## Examples

### Example 1: Basic if with a boolean field

**Goal**: Categorize events as "Success" or "Failure" based on an existing boolean field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_outcome_status = if(is_successful = true, "Success", "Failure") 
| fields event_id, is_successful, event_outcome_status 
| limit 5 
```

**Explanation**: The query evaluates the `is_successful` field. If it is `true`, the new field `event_outcome_status` is set to "Success"; otherwise, it is set to "Failure".

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | EVENT\_OUTCOME\_STATUS |
| --------- | -------------- | ---------------------- |
| 101       | true           | "Success"              |
| 102       | false          | "Failure"              |
| 103       | true           | "Success"              |
| 104       | true           | "Success"              |
| 105       | true           | "Success"              |

### Example 2: if with a numeric comparison

**Goal**: Classify events based on a numerical threshold using the `duration_seconds` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter duration_category = if(duration_seconds > 5.0, "Long Duration", "Short Duration") 
| fields event_id, duration_seconds, duration_category 
| limit 5 
```

**Explanation**: The query checks if `duration_seconds` is greater than 5.0. If true, `duration_category` is labeled "Long Duration"; otherwise, it is labeled "Short Duration".

**Output**:

| EVENT\_ID | DURATION\_SECONDS | DURATION\_CATEGORY |
| --------- | ----------------- | ------------------ |
| 101       | 1.5               | "Short Duration"   |
| 102       | 0.8               | "Short Duration"   |
| 103       | 10.2              | "Long Duration"    |
| 104       | 0.1               | "Short Duration"   |
| 105       | 5.0               | "Short Duration"   |

### Example 3: if with string matching

**Goal**: Categorize `event_id` into distinct ranges using nested conditions to assign a descriptive string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter event_category = if(
    event_id <= 103, "Low Event ID", 
    event_id <= 106, "Medium Event ID", 
    "High Event ID") 
| fields event_id, event_category 
| limit 5 
```

**Explanation**: The query evaluates conditions sequentially. If `event_id` is 103 or less, it assigns "Low Event ID". If that fails but it is 106 or less, it assigns "Medium Event ID". Otherwise, it assigns "High Event ID".

**Output**:

| EVENT\_ID | EVENT\_CATEGORY |
| --------- | --------------- |
| 101       | Low Event ID    |
| 102       | Low Event ID    |
| 103       | Low Event ID    |
| 104       | Medium Event ID |
| 105       | Medium Event ID |

### Example 4: if with nested if for complex logic

**Goal**: Create granular categories based on both the `is_successful` status and `duration_seconds` using nested `if()` functions.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter detailed_status = if( 
    is_successful = true, 
    if(
        duration_seconds > 10.0, 
        "Success - Long Duration", 
        "Success - Short Duration"
    ), 
    "Failure" 
) 
| fields event_id, is_successful, duration_seconds, detailed_status 
| limit 5 
```

**Explanation**: If `is_successful` is true, a nested `if` checks `duration_seconds`. If duration is greater than 10.0, it returns "Success - Long Duration", otherwise "Success - Short Duration". If `is_successful` is false, it returns "Failure".

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | DURATION\_SECONDS | DETAILED\_STATUS           |
| --------- | -------------- | ----------------- | -------------------------- |
| 101       | true           | 1.5               | "Success - Short Duration" |
| 102       | false          | 0.8               | "Failure"                  |
| 103       | true           | 10.2              | "Success - Long Duration"  |
| 104       | true           | 0.1               | "Success - Short Duration" |
| 105       | true           | 5.0               | "Success - Short Duration" |

### Example 5: if returning numeric values with multiplication

**Goal**: Conditionally modify a numeric value using the `multiply()` function based on an event ID threshold.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter threshold_event_id = if(event_id > 104, multiply(event_id, 10), event_id) 
| fields event_id, threshold_event_id 
| limit 5 
```

**Explanation**: If `event_id` is greater than 104, the new field `threshold_event_id` contains the `event_id` multiplied by 10. Otherwise, it contains the original `event_id`.

**Output**:

| EVENT\_ID | THRESHOLD\_EVENT\_ID |
| --------- | -------------------- |
| 101       | 101                  |
| 102       | 102                  |
| 103       | 103                  |
| 104       | 104                  |
| 105       | 1050                 |

### Example 6: if with omitted false return expression

**Goal**: Demonstrate that `if()` returns `NULL` when the condition is false and no false return expression is specified.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter google_traffic_tag = if(dst_domain = "www.google.com", "Google Traffic") 
| fields event_id, dst_domain, google_traffic_tag 
| limit 5 
```

**Explanation**: The query checks if `dst_domain` equals "www.google.com". If true, it returns "Google Traffic". Because no false return value is provided, it returns `NULL` for all other domains.

**Output**:

| EVENT\_ID | DST\_DOMAIN         | GOOGLE\_TRAFFIC\_TAG |
| --------- | ------------------- | -------------------- |
| 101       | "ec2.amazonaws.com" | NULL                 |
| 102       | "sts.amazonaws.com" | NULL                 |
| 103       | "www.google.com"    | "Google Traffic"     |
| 104       | "dropbox.com"       | NULL                 |
| 105       | NULL                | NULL                 |

### Example 7: Remove file extensions conditionally

**Goal**: Use conditional logic to check if a process name contains ".exe" and remove that substring if present, otherwise return the lowercase process name.

**XQL Code**:

```sql
dataset = sample_xql_raw 
| fields action_process_image_name as apin 
| filter apin != null 
| alter remove_exe_process = 
    if(lowercase(apin) contains ".exe",  // boolean expression
       replace(lowercase(apin),".exe",""), // return if true
       lowercase(apin))  // return if false
| limit 10
```

**Explanation**: The query first filters for records where the process image name is not null and aliases it as `apin`. The query then uses the `if()` function to evaluate a boolean expression: whether the lowercase version of the field `apin` contains the string ".exe".

* If the condition is **true**, the `replace()` function is called to find the ".exe" substring and substitute it with an empty string, effectively removing the extension.
* If the condition is **false**, it returns the lowercase name as is. The result of this logic is stored in a new field called `remove_exe_process`.

**Output**:

| apin           | remove\_exe\_process |
| -------------- | -------------------- |
| cmd.exe        | cmd                  |
| POWERSHELL.EXE | powershell           |
| svchost.exe    | svchost              |
| python3        | python3              |

### Example: Categorize local IP addresses using conditional logic

**Goal**: Evaluate the `action_local_ip` field from the last 7 days of `sample_xql_raw` to identify and label specific local IP ranges (10.x.x.x, 172.x.x.x, or 192.168.x.x) in a new column, returning null if no match is found.

**XQL Code**:

```sql
config timeframe = 7d 
| dataset = sample_xql_raw 
| limit 1
| alter 
    check_ip = if(action_local_ip ~= "^10", //boolean expression1
               "Local 10", // true return expression1
               action_local_ip ~= "^172", //boolean expression2
               "Local 172 ?", //true return expression2
               action_local_ip ~= "^192\.168", //boolean expression3
               "Local 192") //true return expression3
```

**Explanation**: The query targets the `sample_xql_raw` dataset for a 7-day period and limits the output to a single record. The query uses the `alter` stage to create a new field, `check_ip`, driven by the `if()` function. The function sequentially evaluates three regular expression matches (`~=`) against the `action_local_ip` field:

* If the IP starts with "10", it returns "Local 10".
* If the first condition is false and the IP starts with "172", it returns "Local 172 ?".
* If the previous conditions are false and the IP starts with "192.168", it returns "Local 192".
* If none of these conditions are met, the function returns `null`.

**Output**:

| action\_local\_ip | check\_ip |
| ----------------- | --------- |
| 192.168.1.50      | Local 192 |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit), [`config`](../stages/config)
* **Functions**: [`multiply`](multiply)
