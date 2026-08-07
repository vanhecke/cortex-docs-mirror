# floor

Use the `floor()` function to convert a field containing a number and return an integer rounded down to the nearest whole number.

## Syntax

```sql
floor (<number>)
```

## Parameters

| Name     | Type           | Required | Description                      |
| -------- | -------------- | -------- | -------------------------------- |
| `number` | integer, float | Yes      | The numeric value to round down. |

## Returns

The `floor()` function returns an integer representing the input number rounded down to the nearest whole number.

## Usage notes

* The function accepts a field that contains a number, meaning it can take integers or floating-point numbers as input.
* The function explicitly rounds the number **down** to the nearest whole integer.
* For positive numbers, this behavior truncates the decimal part (for example, 1.9 becomes 1).
* For negative numbers, it rounds to the next more negative integer (for example, -2.5 becomes -3).

## Examples

### Example 1: Round down positive floating-point field

**Goal**: Round the `duration_seconds` field down to the nearest integer.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter floored_duration = floor(duration_seconds) 
| fields event_id, duration_seconds, floored_duration 
| limit 3 
```

**Explanation**: This query creates a new field, `floored_duration`, by taking the `duration_seconds` (for example, 1.5, 0.8) and rounding it down. For 1.5, it becomes 1; for 0.8, it becomes 0.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | FLOORED\_DURATION |
| --------- | ----------------- | ----------------- |
| 101       | 1.5               | 1                 |
| 102       | 0.8               | 0                 |
| 103       | 10.2              | 10                |

### Example 2: Round down calculated floating-point value

**Goal**: Round the result of a division operation on an integer field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter divided_event_id = divide(event_id, 3) 
| alter floored_divided_id = floor(divided_event_id) 
| fields event_id, divided_event_id, floored_divided_id 
| limit 3 
```

**Explanation**: Here, `event_id` (for example, 101) is divided by 3, resulting in 33.666.... The `floor()` function then rounds this down to 33.

**Output**:

| EVENT\_ID | DIVIDED\_EVENT\_ID | FLOORED\_DIVIDED\_ID |
| --------- | ------------------ | -------------------- |
| 101       | 33.666666          | 33                   |
| 102       | 34.0               | 34                   |
| 103       | 34.333333          | 34                   |

### Example 3: Round down negative number

**Goal**: Round a negative number extracted from an array field to demonstrate rounding towards negative infinity.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_numeric_code = arrayindex(numeric_codes, 1) 
| alter floored_negative_code = floor(first_numeric_code) 
| fields event_id, numeric_codes, first_numeric_code, floored_negative_code 
| limit 3 
```

**Explanation**: For event\_id 101, `first_numeric_code` is -47. The `floor()` of -47 is still -47 as it's an integer. If a negative float like -2.5 were present, `floor()` would convert it to -3.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | FIRST\_NUMERIC\_CODE | FLOORED\_NEGATIVE\_CODE |
| --------- | -------------------------- | -------------------- | ----------------------- |
| 101       | \[13, -47, 29, 82, -15]    | -47                  | -47                     |
| 102       | \[-21, 56, 13, -88, 42]    | 56                   | 56                      |
| 103       | \[90, -33, 7, 51, -62, 18] | -33                  | -33                     |

### Example 4: Round down number extracted from JSON

**Goal**: Round a numeric value extracted from a JSON field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 110 
| alter json_size_string = simple_json_data -> size_gb 
| alter json_size_number = to_number(json_size_string) 
| alter floored_json_size = floor(json_size_number) 
| fields event_id, simple_json_data, json_size_number, floored_json_size 
| limit 1 
```

**Explanation**: This query extracts the `size_gb` value from the `simple_json_data` field (for example, "500" for event\_id 110). The query then converts this string to a number and applies `floor()`, which for an integer like 500 would result in 500.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                        | JSON\_SIZE\_NUMBER | FLOORED\_JSON\_SIZE |
| --------- | ----------------------------------------- | ------------------ | ------------------- |
| 110       | {"backup\_id": "DB-005", "size\_gb": 500} | 500                | 500                 |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit), [`filter`](../stages/filter)
* **Functions**: [`divide`](divide), [`arrayindex`](arrayindex), [`json_extract_scalar`](json_extract_scalar), [`to_number`](to_number)
