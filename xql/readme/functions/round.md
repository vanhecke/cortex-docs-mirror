# round

Use the `round()` function to take a numeric input (either a float or an integer) and return the value rounded to the nearest whole integer.

## Syntax

```sql
round (<float> | <integer>)
```

## Parameters

| Name    | Type           | Required | Description                      |
| ------- | -------------- | -------- | -------------------------------- |
| `value` | float, integer | Yes      | The numeric value to be rounded. |

## Returns

The `round()` function returns an integer representing the input value rounded to the nearest whole number. Standard mathematical rounding rules apply, where values exactly at .5 typically round up.

## Usage notes

* The function accepts either a floating-point number or an integer as its input.
* If the input is already an integer, the value remains unchanged.
* For positive numbers, a fractional part of .5 or greater rounds up to the next higher integer.
* For negative numbers, the function rounds to the nearest integer, adhering to standard mathematical rounding for negative values.

## Examples

### Example 1: Round on a positive floating-point field

**Goal**: Round a positive floating-point field to the nearest integer, demonstrating rounding up and rounding down.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter rounded_duration_up = round(duration_seconds)
| alter example_duration = 1.4
| alter rounded_duration_down = round(example_duration)
| fields event_id, duration_seconds, rounded_duration_up, example_duration, rounded_duration_down
| limit 3
```

**Explanation**: This query calculates `rounded_duration_up` by rounding `duration_seconds`. For `event_id` 101 (`duration_seconds` of 1.5), it rounds to 2. For `event_id` 102 (`duration_seconds` of 0.8), it rounds to 1. A literal 1.4 is introduced to show it rounds down to 1.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | ROUNDED\_DURATION\_UP | EXAMPLE\_DURATION | ROUNDED\_DURATION\_DOWN |
| --------- | ----------------- | --------------------- | ----------------- | ----------------------- |
| 101       | 1.5               | 2                     | 1.4               | 1                       |
| 102       | 0.8               | 1                     | 1.4               | 1                       |
| 103       | 10.2              | 10                    | 1.4               | 1                       |

### Example 2: Round on a calculated floating-point value (from an integer field)

**Goal**: Round a calculated floating-point number derived from an integer field after a division operation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter divided_event_id = divide(event_id, 3)
| alter rounded_divided_id = round(divided_event_id)
| fields event_id, divided_event_id, rounded_divided_id
| limit 3
```

**Explanation**: Here, `event_id` (for example, 101) is divided by 3, resulting in approximately 33.666. The `round()` function then rounds this to 34. For `event_id` 102, 102/3 = 34, so `round()` returns 34.

**Output**:

| EVENT\_ID | DIVIDED\_EVENT\_ID | ROUNDED\_DIVIDED\_ID |
| --------- | ------------------ | -------------------- |
| 101       | 33.666666666666664 | 34                   |
| 102       | 34                 | 34                   |
| 103       | 34                 | 34                   |

### Example 3: Round on a negative floating-point value (from an array field)

**Goal**: Round a negative floating-point number derived from an array element.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter second_numeric_code = arrayindex(numeric_codes, 1)
| alter negative_float_example = divide(second_numeric_code, 10.0)
| alter rounded_negative_float = round(negative_float_example)
| fields event_id, numeric_codes, negative_float_example, rounded_negative_float
| limit 3
```

**Explanation**: For `event_id` 101, `second_numeric_code` is -47. Dividing by 10.0 results in -4.7. `round()` then converts -4.7 to -5. For `event_id` 102, the code is 56, resulting in 5.6, which `round()` converts to 6.

**Output**:

| EVENT\_ID | NUMERIC\_CODES     | NEGATIVE\_FLOAT\_EXAMPLE | ROUNDED\_NEGATIVE\_FLOAT |
| --------- | ------------------ | ------------------------ | ------------------------ |
| 101       | \[13, -47, 29,...] | -4.7                     | -5                       |
| 102       | \[-21, 56, 13,...] | 5.6                      | 6                        |
| 103       | \[90, -33, 7,...]  | -3.3                     | -3                       |

### Example 4: Round on an integer field (no change)

**Goal**: Apply the function to an integer field to confirm that whole numbers remain unchanged.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter rounded_event_id = round(event_id)
| fields event_id, rounded_event_id
| limit 3
```

**Explanation**: The `event_id` field contains integers (for example, 101, 102). When `round()` is applied, these values remain 101, 102, etc., demonstrating no change for whole numbers.

**Output**:

| EVENT\_ID | ROUNDED\_EVENT\_ID |
| --------- | ------------------ |
| 101       | 101                |
| 102       | 102                |
| 103       | 103                |

### Example 5: Round on a numeric value extracted from JSON data

**Goal**: Round a number extracted from a JSON field after converting it and performing a calculation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter simple_json_data != null
| alter json_code_string = simple_json_data -> code
| alter json_numeric_value = to_number(json_code_string)
| alter calc_json_value = divide(json_numeric_value, 1.5)
| alter rounded_json_value = round(calc_json_value)
| fields event_id, simple_json_data, json_numeric_value, calc_json_value, rounded_json_value
| limit 1
```

**Explanation**: This query extracts the `code` value (for example, "200") from the `simple_json_data` field as a string, converts it to a number using `to_number()`, divides it by 1.5 to introduce a decimal, and then applies `round()` to get the nearest whole integer. Note that only `event_id` 101 has a "code" field in `simple_json_data` in the `sample_xql_raw` dataset, hence only one result is displayed.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA            | JSON\_NUMERIC\_VALUE | CALC\_JSON\_VALUE  | ROUNDED\_JSON\_VALUE |
| --------- | ----------------------------- | -------------------- | ------------------ | -------------------- |
| 101       | {"status": "ok", "code": 200} | 200                  | 133.33333333333334 | 133                  |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`divide`](divide), [`arrayindex`](arrayindex), [`to_number`](to_number)
