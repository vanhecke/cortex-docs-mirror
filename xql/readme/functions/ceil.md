# ceil

Use the `ceil()` function to convert a field containing a number and return an integer rounded up to the nearest whole number.

## Syntax

```sql
ceil (<number>)
```

## Parameters

| Name     | Type           | Required | Description                    |
| -------- | -------------- | -------- | ------------------------------ |
| `number` | integer, float | Yes      | The numeric value to round up. |

## Returns

The `ceil()` function returns an integer representing the input number rounded up to the nearest whole number.

## Usage notes

* The function accepts a field that contains a number, meaning it can take integers or floating-point numbers as input.
* The function explicitly rounds the number **up** to the nearest whole integer.
* For positive numbers, this behavior rounds up past the decimal part (for example, 1.1 becomes 2).
* For negative numbers, it rounds toward zero (for example, -2.5 becomes -2).

## Examples

### Example 1: Round up positive floating-point field

**Goal**: Round the `duration_seconds` field up to the nearest integer.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter ceiled_duration = ceil(duration_seconds) 
| fields event_id, duration_seconds, ceiled_duration 
| limit 3 
```

**Explanation**: This query creates a new field, `ceiled_duration`, by taking the `duration_seconds` (for example, 1.5, 0.8) and rounding it up. For 1.5, it becomes 2; for 0.8, it becomes 1.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | CEILED\_DURATION |
| --------- | ----------------- | ---------------- |
| 101       | 1.5               | 2                |
| 102       | 0.8               | 1                |
| 103       | 10.2              | 11               |

### Example 2: Round up calculated floating-point value

**Goal**: Round the result of a division operation on an integer field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter divided_event_id = divide(event_id, 3) 
| alter ceiled_divided_id = ceil(divided_event_id) 
| fields event_id, divided_event_id, ceiled_divided_id 
| limit 3 
```

**Explanation**: Here, `event_id` (for example, 101) is divided by 3, resulting in 33.666.... The `ceil()` function then rounds this up to 34.

**Output**:

| EVENT\_ID | DIVIDED\_EVENT\_ID | CEILED\_DIVIDED\_ID |
| --------- | ------------------ | ------------------- |
| 101       | 33.666666          | 34                  |
| 102       | 34.0               | 34                  |
| 103       | 34.333333          | 35                  |

### Example 3: Round up negative number

**Goal**: Round a negative floating-point number to demonstrate rounding towards zero.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter negative_value = subtract(0, duration_seconds) 
| alter ceiled_negative = ceil(negative_value) 
| fields event_id, duration_seconds, negative_value, ceiled_negative 
| limit 3 
```

**Explanation**: This query negates the `duration_seconds` field and then applies `ceil()`. For a negative value like -1.5, `ceil()` rounds toward zero, resulting in -1. For -0.8, it becomes 0.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | NEGATIVE\_VALUE | CEILED\_NEGATIVE |
| --------- | ----------------- | --------------- | ---------------- |
| 101       | 1.5               | -1.5            | -1               |
| 102       | 0.8               | -0.8            | 0                |
| 103       | 10.2              | -10.2           | -10              |

### Example 4: Round up number extracted from JSON

**Goal**: Round a numeric value extracted from a JSON field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 110 
| alter json_size_string = simple_json_data -> size_gb 
| alter json_size_number = to_number(json_size_string) 
| alter ceiled_json_size = ceil(json_size_number) 
| fields event_id, simple_json_data, json_size_number, ceiled_json_size 
| limit 1 
```

**Explanation**: This query extracts the `size_gb` value from the `simple_json_data` field (for example, "500" for event\_id 110). The query then converts this string to a number and applies `ceil()`, which for an integer like 500 would result in 500.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                        | JSON\_SIZE\_NUMBER | CEILED\_JSON\_SIZE |
| --------- | ----------------------------------------- | ------------------ | ------------------ |
| 110       | {"backup\_id": "DB-005", "size\_gb": 500} | 500                | 500                |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit), [`filter`](../stages/filter)
* **Functions**: [`floor`](floor), [`round`](round), [`divide`](divide), [`subtract`](subtract), [`to_number`](to_number)
