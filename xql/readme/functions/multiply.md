# multiply

Use the `multiply()` function to calculate the product of two numbers.

## Syntax

```sql
multiply (<string> | <integer> | <float>, <string> | <integer> | <float>)
```

## Parameters

| Name      | Type                   | Required | Description               |
| --------- | ---------------------- | -------- | ------------------------- |
| `value_1` | integer, float, string | Yes      | The first numeric value.  |
| `value_2` | integer, float, string | Yes      | The second numeric value. |

## Returns

The `multiply()` function returns the numerical product of the two input numbers.

## Usage notes

* The function accepts various numeric inputs, including numeric literals (for example, 2, 1.5), floating-point numbers, and integers.
* The function also accepts integers or numbers provided as a string type (for example, extracted from a data field and then converted).
* The function supports negative numbers for both input parameters.

## Examples

### Example 1: Multiply integer field by integer literal

**Goal**: Demonstrate `multiply()` applied directly to an integer field (`event_id`) and a fixed integer literal.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter multiplied_event_id = multiply(event_id, 2) 
| fields event_id, multiplied_event_id 
| limit 3 
```

**Explanation**: This query creates a new field, `multiplied_event_id`, by taking each `event_id` (for example, 101) and multiplying it by 2.

**Output**:

| EVENT\_ID | MULTIPLIED\_EVENT\_ID |
| --------- | --------------------- |
| 101       | 202                   |
| 102       | 204                   |
| 103       | 206                   |

### Example 2: Multiply floating-point field by integer literal

**Goal**: Showcase `multiply()` with a floating-point input field (`duration_seconds`) and an integer literal.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter multiplied_duration = multiply(duration_seconds, 10) 
| fields event_id, duration_seconds, multiplied_duration 
| limit 3 
```

**Explanation**: Here, `duration_seconds` (which contains decimal values, for example, 1.5, 0.8) is multiplied by 10, producing a new floating-point value in `multiplied_duration`.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | MULTIPLIED\_DURATION |
| --------- | ----------------- | -------------------- |
| 101       | 1.5               | 15.0                 |
| 102       | 0.8               | 8.0                  |
| 103       | 10.2              | 102.0                |

### Example 3: Multiply floating-point field by floating-point literal

**Goal**: Demonstrate `multiply()` handling two floating-point numbers, including a decimal literal.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter precise_duration_calc = multiply(duration_seconds, 0.75) 
| fields event_id, duration_seconds, precise_duration_calc 
| limit 3 
```

**Explanation**: This query multiplies `duration_seconds` by 0.75, resulting in `precise_duration_calc`, which will also be a floating-point number.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | PRECISE\_DURATION\_CALC |
| --------- | ----------------- | ----------------------- |
| 101       | 1.5               | 1.125                   |
| 102       | 0.8               | 0.6                     |
| 103       | 10.2              | 7.65                    |

### Example 4: Multiply with a negative integer literal

**Goal**: Demonstrate `multiply()` handling a negative input, producing a negative result.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter negative_event_id = multiply(event_id, -1) 
| fields event_id, negative_event_id 
| limit 3 
```

**Explanation**: The `event_id` is multiplied by -1. This correctly computes the negative product, demonstrating the function's behavior with negative inputs.

**Output**:

| EVENT\_ID | NEGATIVE\_EVENT\_ID |
| --------- | ------------------- |
| 101       | -101                |
| 102       | -102                |
| 103       | -103                |

### Example 5: Multiply string-converted-to-number field by integer literal

**Goal**: Show `multiply()` applied to a numeric value extracted from a JSON field and converted from a string, demonstrating flexibility with input types.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id in (101, 110) 
| alter json_numeric_string = coalesce(simple_json_data -> code, simple_json_data -> size_gb) 
| alter json_numeric_value = to_number(json_numeric_string) 
| alter multiplied_json_value = multiply(json_numeric_value, 3) 
| fields event_id, simple_json_data, json_numeric_value, multiplied_json_value 
| limit 3 
```

**Explanation**: This query first extracts a numeric value (either `code` or `size_gb`) from the `simple_json_data` field as a string. The query then converts this string to a number using `to_number()` and applies `multiply()` with a literal, storing the result in `multiplied_json_value`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA                        | JSON\_NUMERIC\_VALUE | MULTIPLIED\_JSON\_VALUE |
| --------- | ----------------------------------------- | -------------------- | ----------------------- |
| 101       | {"status": "ok", "code": 200}             | 200                  | 600                     |
| 110       | {"backup\_id": "DB-005", "size\_gb": 500} | 500                  | 1500                    |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`to_number`](to_number), [`coalesce`](coalesce)
