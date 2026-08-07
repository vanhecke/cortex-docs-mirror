# cot

Use the `cot()` function to calculate the cotangent of a numeric value specified in radians. The cotangent is the reciprocal of the tangent function.

## Syntax

```sql
cot(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                                               |
| -------------------- | -------------- | -------- | --------------------------------------------------------------------------------------------------------- |
| `numeric_expression` | integer, float | Yes      | The angle in radians for which to calculate the cotangent. The value must not be zero or a multiple of π. |

## Returns

**Type**: float

**Description**: The `cot()` function returns the cotangent of the input angle, which is equivalent to `cos(x) / sin(x)` or `1 / tan(x)`. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `cot()` function accepts any real number except values where `sin(x) = 0` (i.e., multiples of π), where the cotangent is undefined.
* **Undefined Values**: At `x = 0` and multiples of π, the function returns `infinity`, `NaN`, or `null` since the cotangent is undefined at these points.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Relationship**: `cot(x) = 1 / tan(x) = cos(x) / sin(x)`.
* **Common Use Cases**: This function is typically used within the `alter` stage for trigonometric calculations, geometric analysis, and engineering computations.

## Examples

### Example 1: Calculate cotangent of literal values

**Goal**: Calculate the cotangent for specific radian values to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = cot(divide(pi(), 4)), result2 = cot(divide(pi(), 2)), result3 = cot(1)
| fields result1, result2, result3
```

**Explanation**: You use `cot()` on three different radian values. `cot(π/4)` returns `1.0` (since `tan(π/4) = 1`), `cot(π/2)` returns approximately `0.0` (since `tan(π/2)` approaches infinity), and `cot(1)` returns approximately `0.6421`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 1.0     | 0.0     | 0.64209 |

### Example 2: Calculate cotangent from a field value

**Goal**: Calculate the cotangent of values stored in a dataset field, filtering out values near zero.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value != 0
| alter cot_val = cot(numeric_value)
| fields event_id, numeric_value, cot_val
| limit 3
```

**Explanation**: This query filters out zero values (where cotangent is undefined), then computes the cotangent for each remaining value in the `numeric_value` field.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | COT\_VAL |
| --------- | -------------- | -------- |
| 101       | 0.5            | 1.83049  |
| 102       | 1.0            | 0.64209  |
| 103       | 2.0            | -0.45766 |

### Example 3: Verify cotangent as reciprocal of tangent

**Goal**: Demonstrate that `cot(x)` equals `1 / tan(x)` by computing both and comparing.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value != 0
| alter cot_val = cot(numeric_value)
| alter reciprocal_tan = divide(1, tan(numeric_value))
| fields event_id, numeric_value, cot_val, reciprocal_tan
| limit 3
```

**Explanation**: This query computes both `cot(numeric_value)` and `1 / tan(numeric_value)` to verify they produce the same result, confirming the mathematical identity `cot(x) = 1 / tan(x)`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | COT\_VAL | RECIPROCAL\_TAN |
| --------- | -------------- | -------- | --------------- |
| 101       | 0.5            | 1.83049  | 1.83049         |
| 102       | 1.0            | 0.64209  | 0.64209         |
| 103       | 2.0            | -0.45766 | -0.45766        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`tan()`](tan), [`cos()`](cos), [`sin()`](sin), `coth()`
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
