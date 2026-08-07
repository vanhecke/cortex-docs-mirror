# sec

Use the `sec()` function to calculate the secant of a numeric value specified in radians. The secant is the reciprocal of the cosine function.

## Syntax

```sql
sec(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                                           |
| -------------------- | -------------- | -------- | ----------------------------------------------------------------------------------------------------- |
| `numeric_expression` | integer, float | Yes      | The angle in radians for which to calculate the secant. The value must not be an odd multiple of p/2. |

## Returns

**Type**: float

**Description**: The `sec()` function returns the secant of the input angle, which is equivalent to `1 / cos(x)`. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `sec()` function accepts any real number except values where `cos(x) = 0` (i.e., odd multiples of p/2), where the secant is undefined.
* **Undefined Values**: At odd multiples of p/2 (for example, p/2, 3p/2), the function returns `infinity`, `NaN`, or `null` since the secant is undefined at these points.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Relationship**: `sec(x) = 1 / cos(x)`.
* **Result Range**: The result is always = -1 or = 1 (never between -1 and 1).
* **Common Use Cases**: This function is typically used within the `alter` stage for trigonometric calculations, optics computations, and engineering analysis.

## Examples

### Example 1: Calculate secant of literal values

**Goal**: Calculate the secant for specific radian values to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = sec(0), result2 = sec(pi()), result3 = sec(1)
| fields result1, result2, result3
```

**Explanation**: `sec(0)` returns `1.0` (since `cos(0) = 1`), `sec(p)` returns `-1.0` (since `cos(p) = -1`), and `sec(1)` returns approximately `1.8508`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 1.0     | -1.0    | 1.85082 |

### Example 2: Calculate secant from a field value

**Goal**: Calculate the secant of values stored in a dataset field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter sec_val = sec(numeric_value)
| fields event_id, numeric_value, sec_val
| limit 3
```

**Explanation**: This query computes the secant for each value in the `numeric_value` field and stores the result in `sec_val`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SEC\_VAL |
| --------- | -------------- | -------- |
| 101       | 0.0            | 1.0      |
| 102       | 1.0            | 1.85082  |
| 103       | 3.14159        | -1.0     |

### Example 3: Verify secant as reciprocal of cosine

**Goal**: Demonstrate that `sec(x)` equals `1 / cos(x)` by computing both and comparing.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter sec_val = sec(numeric_value)
| alter reciprocal_cos = divide(1, cos(numeric_value))
| fields event_id, numeric_value, sec_val, reciprocal_cos
| limit 3
```

**Explanation**: This query computes both `sec(numeric_value)` and `1 / cos(numeric_value)` to verify they produce the same result, confirming the mathematical identity `sec(x) = 1 / cos(x)`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SEC\_VAL | RECIPROCAL\_COS |
| --------- | -------------- | -------- | --------------- |
| 101       | 0.0            | 1.0      | 1.0             |
| 102       | 1.0            | 1.85082  | 1.85082         |
| 103       | 3.14159        | -1.0     | -1.0            |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`cos()`](cos), [`csc()`](csc), `sech()`, [`cot()`](cot)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
