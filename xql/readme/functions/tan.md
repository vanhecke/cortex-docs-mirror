# tan

Use the `tan()` function to calculate the tangent of a numeric value specified in radians.

## Syntax

```sql
tan(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                                                                                 |
| -------------------- | -------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `numeric_expression` | integer, float | Yes      | The angle in radians for which to calculate the tangent. Any real number is valid, though the tangent is undefined at odd multiples of p/2. |

## Returns

**Type**: float

**Description**: The `tan()` function returns the tangent of the input angle. The result can be any real number. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `tan()` function accepts any real number as input. The input is interpreted as an angle in radians.
* **Undefined Values**: At odd multiples of p/2 (for example, p/2, 3p/2), the tangent is mathematically undefined and the function may return a very large number, `infinity`, or `NaN`.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Degrees to Radians**: If your input is in degrees, convert it to radians first by multiplying by `PI() / 180`.
* **Periodicity**: The tangent function is periodic with period p, meaning `tan(x) = tan(x + p)`.
* **Key Values**: `tan(0)` returns `0.0`, `tan(p/4)` returns `1.0`, `tan(p)` returns `0.0`.
* **Symmetry**: The function is odd, meaning `tan(-x) = -tan(x)`.
* **Common Use Cases**: This function is typically used within the `alter` stage for trigonometric calculations, slope computations, angle analysis, and engineering formulas.

## Examples

### Example 1: Calculate tangent of literal values

**Goal**: Calculate the tangent for specific radian values to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = tan(0), result2 = tan(divide(pi(), 4)), result3 = tan(pi())
| fields result1, result2, result3
```

**Explanation**: `tan(0)` returns `0.0`, `tan(p/4)` returns `1.0` (since sine and cosine are equal at p/4), and `tan(p)` returns approximately `0.0`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 0.0     | 1.0     | 0.0     |

### Example 2: Calculate tangent from a field value

**Goal**: Calculate the tangent of values stored in a dataset field, treating them as angles in radians.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter tan_val = tan(numeric_value)
| fields event_id, numeric_value, tan_val
| limit 3
```

**Explanation**: This query computes the tangent for each value in the `numeric_value` field and stores the result in `tan_val`. Since `tan()` accepts any real number, no filtering is needed.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | TAN\_VAL |
| --------- | -------------- | -------- |
| 101       | 0.0            | 0.0      |
| 102       | 0.7854         | 1.0      |
| 103       | 1.0            | 1.55741  |

### Example 3: Calculate slope angle from rise and run

**Goal**: Use the tangent function to verify a slope calculation by computing `tan(atan(rise/run))`.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter duration_seconds > 0
| alter slope = divide(numeric_value, duration_seconds)
| alter angle = atan(slope)
| alter tan_angle = tan(angle)
| fields event_id, numeric_value, duration_seconds, slope, tan_angle
| limit 3
```

**Explanation**: This query calculates the slope as `numeric_value / duration_seconds`, then computes the angle using `atan()`, and finally verifies by computing `tan()` of that angle. The `tan_angle` should match the original `slope`, confirming the identity `tan(atan(x)) = x`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | SLOPE | TAN\_ANGLE |
| --------- | -------------- | ----------------- | ----- | ---------- |
| 101       | 3.0            | 4.0               | 0.75  | 0.75       |
| 102       | 5.0            | 1.0               | 5.0   | 5.0        |
| 103       | 10.0           | 10.0              | 1.0   | 1.0        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: `atan()`, [`sin()`](sin), [`cos()`](cos), [`cot()`](cot), `pi()`
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
