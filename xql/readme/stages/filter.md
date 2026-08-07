# filter

Use the `filter` stage to precisely narrow down the data records returned by your query. The stage identifies which records should be included in the result set by evaluating boolean expressions. If a record satisfies the filter condition (i.e., the expression returns `true`), it is returned; otherwise, it is excluded.

## Syntax

```sql
filter <boolean_expression>
```

## Parameters

| Name                 | Type    | Required | Description                                                                                                                                    |
| -------------------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `boolean_expression` | boolean | Yes      | A logical expression that evaluates to `true` or `false`. Only records where this expression evaluates to `true` are passed to the next stage. |

## Returns

The `filter` stage returns a subset of the original dataset containing only the records for which the boolean expression evaluates to `true`.

## Usage notes

* Applying the `filter` stage as early as possible in your query is a best practice. This significantly reduces the dataset size for subsequent stages, improving performance and reducing processing cost, especially with large datasets.
* The `filter` stage supports various operators to express diverse filtering conditions, including comparison operators (`=`, `!=`, `<`, `<=`, `>`, `>=`), boolean operators (`and`, `or`, `not`), and string/range operators (`in`, `not in`, `contains`, `~=`, `!~=`, `incidr`, `incidr6`).
* Parentheses `()` can be used to explicitly define the order of evaluation for logical conditions.
* Filters can check for the presence or absence of values using `null` or empty string `""`.
* XQL treats string values differently based on whether single (`"`) or triple (`"""`) double quotes are used. Single double quotes treat the string literally (where `*` matches any sequence), while triple double quotes enable regex-style pattern matching and escape sequence interpretation.
* You can employ subqueries within the `filter` stage, particularly with the `in` or `not in` operators, to define a list of values for comparison derived from another dataset or subset.
* Functions can be used within filters (for example, `to_number()`, `json_extract_scalar()`) for complex data transformations and evaluations during the filtering process.

## Examples

### Example 1: Comparison operator - equals (=)

**Goal**: Filter for records where the `event_id` is exactly 101.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id = 101
| fields event_id, event_description
```

**Explanation**: Returns `true` if the field value is exactly equal to the specified value.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      |
| --------- | ----------------------- |
| 101       | "User login successful" |

### Example 2: Comparison operator - not equal to (!=)

**Goal**: Filter for records where the `is_successful` field is not true.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter is_successful != true
| fields event_id, is_successful
```

**Explanation**: Returns `true` if the field value is not equal to the specified value.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL |
| --------- | -------------- |
| 102       | false          |
| 106       | false          |
| 109       | false          |

### Example 3: Comparison operator -less than (<)

**Goal**: Filter for records where `duration_seconds` is strictly less than 1.0.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter duration_seconds < 1.0
| fields event_id, duration_seconds
```

**Explanation**: Returns `true` if the numeric field value is strictly less than the specified value.

**Output**:

| EVENT\_ID | DURATION\_SECONDS |
| --------- | ----------------- |
| 104       | 0.1               |
| 109       | 0.05              |

### Example 4: Comparison operator - less than or equal to (<=)

**Goal**: Filter for records where the extracted JSON status code is less than or equal to 200.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter to_number(json_extract_scalar(simple_json_data, "$.code")) <= 200
| fields event_id, simple_json_data
```

**Explanation**: Returns `true` if the numeric field value is less than or equal to the specified value.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                            |
| --------- | --------------------------------------------- |
| 101       | {"status": "ok", "code": 200}                 |
| 102       | {"status": "fail", "error": "access\_denied"} |

### Example 5: Comparison operator - greater than (>)

**Goal**: Filter for records where `duration_seconds` is strictly greater than 5.0.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter duration_seconds > 5.0
| fields event_id, duration_seconds
```

**Explanation**: Returns `true` if the numeric field value is strictly greater than the specified value.

**Output**:

| EVENT\_ID | DURATION\_SECONDS |
| --------- | ----------------- |
| 103       | 10.2              |
| 107       | 7.8               |
| 108       | 15.3              |
| 110       | 60.0              |

### Example 6: Comparison operator - greater than or equal to (>=)

**Goal**: Filter for records where the extracted JSON status code is greater than or equal to 200.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter to_number(json_extract_scalar(simple_json_data, "$.code")) >= 200
| fields event_id, simple_json_data
```

**Explanation**: Returns `true` if the numeric field value is greater than or equal to the specified value.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA            |
| --------- | ----------------------------- |
| 101       | {"status": "ok", "code": 200} |

### Example 7: Boolean operator - AND (and)

**Goal**: Filter for records where `is_successful` is true AND `duration_seconds` is greater than 5.0.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter is_successful = true and duration_seconds > 5.0
| fields event_id, is_successful, duration_seconds
```

**Explanation**: Returns `true` only if **all** conditions separated by `and` are met.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL | DURATION\_SECONDS |
| --------- | -------------- | ----------------- |
| 103       | true           | 10.2              |
| 107       | true           | 7.8               |
| 108       | true           | 15.3              |
| 110       | true           | 60.0              |

### Example 8: Boolean operator - OR (or)

**Goal**: Filter for records where `event_description` is "User login successful" OR `is_successful` is false.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_description = "User login successful" or is_successful = false
| fields event_id, event_description, is_successful
```

**Explanation**: Returns `true` if **any** of the conditions separated by `or` are met.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             | IS\_SUCCESSFUL |
| --------- | ------------------------------ | -------------- |
| 101       | "User login successful"        | true           |
| 102       | "File access attempt"          | false          |
| 106       | "Unauthorized access detected" | false          |
| 109       | "API request throttled"        | false          |

### Example 9: Boolean operator - NOT (not)

**Goal**: Filter for records where `is_successful` is NOT true.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter not is_successful = true
| fields event_id, is_successful
```

**Explanation**: Returns `true` if the condition immediately following `not` is **not** met.

**Output**:

| EVENT\_ID | IS\_SUCCESSFUL |
| --------- | -------------- |
| 102       | false          |
| 106       | false          |
| 109       | false          |

### Example 10: Boolean operator - parentheses grouping

**Goal**: Filter for records where the description is either "User login successful" or "System heartbeat", AND `is_successful` is true.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter (event_description = "User login successful" or event_description = "System heartbeat") and is_successful = true
| fields event_id, event_description, is_successful
```

**Explanation**: Parentheses explicitly define the order of evaluation for logical conditions.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      | IS\_SUCCESSFUL |
| --------- | ----------------------- | -------------- |
| 101       | "User login successful" | true           |
| 104       | "System heartbeat"      | true           |

### Example 11: String operator - IN (in)

**Goal**: Filter for records where `event_description` matches any value in the provided list.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_description in ("User login successful", "Network connection established")
| fields event_id, event_description
```

**Explanation**: Checks if a field's value is present within a provided list.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               |
| --------- | -------------------------------- |
| 101       | "User login successful"          |
| 103       | "Network connection established" |

### Example 12: String operator - NOT IN (not in)

**Goal**: Filter for records where `event_description` does NOT match any pattern in the provided list.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_description not in ("*heartbeat*", "*transformation*")
| fields event_id, event_description
```

**Explanation**: Checks if a field's value is not present within a provided list. Supports wildcards (`*`) for string values.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               |
| --------- | -------------------------------- |
| 101       | "User login successful"          |
| 102       | "File access attempt"            |
| 103       | "Network connection established" |
| 106       | "Unauthorized access detected"   |
| 107       | "Cloud resource modification"    |
| 108       | "Software update initiated"      |
| 109       | "API request throttled"          |
| 110       | "Database backup completed"      |

### Example 13: String operator - contains

**Goal**: Filter for records where `raw_log_data` contains the substring "Process".

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter raw_log_data contains "Process"
| fields event_id, raw_log_data
```

**Explanation**: Returns `true` if the string field value contains the specified substring.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                    |
| --------- | ------------------------------------------------- |
| 102       | "Process cmd.exe attempted to access /etc/passwd" |

### Example 14: Regular expression match (\~=)

**Goal**: Filter for records where `event_description` matches a regex pattern for login success or failure.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_description ~= ".*login (?:successful|failed).*"
| fields event_id, event_description
```

**Explanation**: Returns `true` if the regular expression matches.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             |
| --------- | ------------------------------ |
| 101       | "User login successful"        |
| 106       | "Unauthorized access detected" |

### Example 15: Regular expression does not match (!\~=)

**Goal**: Filter for records where `event_description` does NOT match a case-insensitive regex pattern for system heartbeat or update.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter not event_description ~= "(?i).*system (?:heartbeat|update).*"
| fields event_id, event_description
```

**Explanation**: Returns `true` if the regular expression does **not** match.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               |
| --------- | -------------------------------- |
| 101       | "User login successful"          |
| 102       | "File access attempt"            |
| 103       | "Network connection established" |
| 105       | "Data transformation"            |
| 106       | "Unauthorized access detected"   |
| 109       | "API request throttled"          |
| 110       | "Database backup completed"      |

### Example 16: Range operator - incidr (IPv4)

**Goal**: Filter for records where `ipv4_address` falls within the `192.168.1.0/24` CIDR range.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter ipv4_address incidr "192.168.1.0/24"
| fields event_id, ipv4_address
```

**Explanation**: Returns `true` if an IPv4 address falls within specified CIDR ranges.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS  |
| --------- | -------------- |
| 101       | "192.168.1.10" |

### Example 17: Range operator - not incidr (IPv4)

**Goal**: Filter for records where `ipv4_address` does NOT fall within typical private IP ranges.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter ipv4_address not incidr "10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16"
| fields event_id, ipv4_address
```

**Explanation**: Returns `true` if an IPv4 address does not fall within the specified CIDR ranges.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS  |
| --------- | -------------- |
| 106       | "203.0.113.15" |

### Example 18: Range operator - incidr6 (IPv6)

**Goal**: Filter for records where `ipv6_address` falls within the `2001:0db8::/32` CIDR range.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter ipv6_address incidr6 "2001:0db8::/32"
| fields event_id, ipv6_address
```

**Explanation**: Returns `true` if an IPv6 address falls within specified CIDR6 ranges.

**Output**:

| EVENT\_ID | IPV6\_ADDRESS          |
| --------- | ---------------------- |
| 103       | "2001:0db8::1"         |
| 107       | "2001:0db8:cafe::1"    |
| 109       | "2001:0db8:1234::abcd" |

### Example 19: Range operator - not incidr6 (IPv6)

**Goal**: Filter for records where `ipv6_address` does NOT fall within the `fe80::/10` CIDR range.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter ipv6_address not incidr6 "fe80::/10"
| fields event_id, ipv6_address
```

**Explanation**: Returns `true` if an IPv6 address does not fall within the specified CIDR6 range.

**Output**:

| EVENT\_ID | IPV6\_ADDRESS          |
| --------- | ---------------------- |
| 103       | "2001:0db8::1"         |
| 107       | "2001:0db8:cafe::1"    |
| 109       | "2001:0db8:1234::abcd" |

### Example 20: Null value filtering (AND)

**Goal**: Filter for records where `ipv6_address` is neither null nor empty.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter ipv6_address != null and ipv6_address != ""
| fields event_id, ipv6_address
```

**Explanation**: Filters out records where a field is `null` or an empty string `""`.

**Output**:

| EVENT\_ID | IPV6\_ADDRESS          |
| --------- | ---------------------- |
| 103       | "2001:0db8::1"         |
| 107       | "2001:0db8:cafe::1"    |
| 109       | "2001:0db8:1234::abcd" |

### Example 21: Null value filtering (NOT IN)

**Goal**: Filter for records where `ipv6_address` is not in the set of null or empty strings.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter ipv6_address not in("", null)
| fields event_id, ipv6_address
```

**Explanation**: An alternative way to filter out nulls or empty strings using the `not in` operator.

**Output**:

| EVENT\_ID | IPV6\_ADDRESS          |
| --------- | ---------------------- |
| 103       | "2001:0db8::1"         |
| 107       | "2001:0db8:cafe::1"    |
| 109       | "2001:0db8:1234::abcd" |

### Example 22: String manipulation - single quotes

**Goal**: Filter using single double quotes (`"text"`) where wildcards behave normally.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_description = "User login*"
| fields event_id, event_description
```

**Explanation**: Treats the string value literally. Wildcards (`*`) match any sequence of characters. Escape sequences are treated as plain characters.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION      |
| --------- | ----------------------- |
| 101       | "User login successful" |

### Example 23: String manipulation - triple quotes

**Goal**: Filter using triple double quotes (`"""text"""`) to enable regex-style pattern matching.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter raw_log_data = """Process cmd.exe*passwd"""
| fields event_id, raw_log_data
```

**Explanation**: Enables regex-style pattern matching and escape sequence interpretation. Wildcards (`*`) still act as XQL wildcards.

**Output**:

| EVENT\_ID | RAW\_LOG\_DATA                                    |
| --------- | ------------------------------------------------- |
| 102       | "Process cmd.exe attempted to access /etc/passwd" |

### Example 24: Subquery filtering - IN

**Goal**: Filter for events in the main dataset whose IDs are found in a specific subset of successful events (using a subquery).

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id in (
    dataset = sample_xql_raw
    | filter is_successful = true and duration_seconds > 5.0
    | fields event_id
)
| fields event_id, event_description, is_successful, duration_seconds
```

**Explanation**: The inner query identifies `event_id`s where `is_successful` is `true` AND `duration_seconds` > 5.0. The outer `filter` then includes only records from the main dataset that have these `event_id`s.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | IS\_SUCCESSFUL | DURATION\_SECONDS |
| --------- | -------------------------------- | -------------- | ----------------- |
| 103       | "Network connection established" | true           | 10.2              |
| 107       | "Cloud resource modification"    | true           | 7.8               |
| 108       | "Software update initiated"      | true           | 15.3              |
| 110       | "Database backup completed"      | true           | 60.0              |

### Example 25: Subquery filtering - NOT IN

**Goal**: Exclude events whose IDs are found in a specific subset of unsuccessful events (using a subquery).

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id not in (
    dataset = sample_xql_raw
    | filter is_successful = false and duration_seconds < 1.0
    | fields event_id
)
| fields event_id, event_description, is_successful, duration_seconds
```

**Explanation**: The inner query identifies `event_id`s where `is_successful` is `false` AND `duration_seconds` < 1.0. The outer `filter` includes all records except those with these specific `event_id`s (102 and 109).

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION               | IS\_SUCCESSFUL | DURATION\_SECONDS |
| --------- | -------------------------------- | -------------- | ----------------- |
| 101       | "User login successful"          | true           | 1.5               |
| 103       | "Network connection established" | true           | 10.2              |
| 104       | "System heartbeat"               | true           | 0.1               |
| 105       | "Data transformation"            | true           | 5.0               |
| 106       | "Unauthorized access detected"   | false          | 2.1               |
| 107       | "Cloud resource modification"    | true           | 7.8               |
| 108       | "Software update initiated"      | true           | 15.3              |
| 110       | "Database backup completed"      | true           | 60.0              |

## Related articles

* **Stages**: [`alter`](alter), [`fields`](fields), [`config`](config), [`limit`](limit)
* **Functions**: [`to_number`](../functions/to_number), [`json_extract_scalar`](../functions/json_extract_scalar)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
