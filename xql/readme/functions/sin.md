# sin

Use the `sin()` function to calculate the sine of a numeric value specified in radians.

## Syntax

```sql
sin(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                     |
| -------------------- | -------------- | -------- | ------------------------------------------------------------------------------- |
| `numeric_expression` | integer, float | Yes      | The angle in radians for which to calculate the sine. Any real number is valid. |

## Returns

**Type**: float

**Description**: The `sin()` function returns the sine of the input angle. The resulting value is within the range \[-1, 1].

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `sin()` function accepts any real number as input. The input is interpreted as an angle in radians.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Degrees to Radians**: If your input is in degrees, convert it to radians first by multiplying by `PI() / 180`.
* **Periodicity**: The sine function is periodic with period 2π, meaning `sin(x) = sin(x + 2π)`.
* **Key Values**: `sin(0)` returns `0.0`, `sin(π/2)` returns `1.0`, `sin(π)` returns `0.0`, `sin(3π/2)` returns `-1.0`.
* **Symmetry**: The function is odd, meaning `sin(-x) = -sin(x)`.
* **Common Use Cases**: This function is typically used within the `alter` stage for trigonometric calculations, signal processing, coordinate transformations, and wave analysis.

## Examples

### Example 1: Calculate sine of literal values

**Goal**: Calculate the sine for specific radian values to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = sin(0), result2 = sin(divide(pi(), 2)), result3 = sin(pi())
| fields result1, result2, result3
```

**Explanation**: `sin(0)` returns `0.0`, `sin(π/2)` returns `1.0`, and `sin(π)` returns approximately `0.0` (a very small number close to zero due to floating-point precision).

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 0.0     | 1.0     | 0.0     |

### Example 2: Calculate sine from a field value

**Goal**: Calculate the sine of values stored in a dataset field, treating them as angles in radians.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter sin_val = sin(numeric_value)
| fields event_id, numeric_value, sin_val
| limit 3
```

**Explanation**: This query computes the sine for each value in the `numeric_value` field and stores the result in `sin_val`. Since `sin()` accepts any real number, no filtering is needed.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SIN\_VAL |
| --------- | -------------- | -------- |
| 101       | 0.0            | 0.0      |
| 102       | 1.5708         | 1.0      |
| 103       | 3.14159        | 0.0      |

### Example 3: Use sine in a coordinate transformation

**Goal**: Use the sine function to compute the y-component of a polar-to-Cartesian coordinate transformation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter y_component = multiply(numeric_value, sin(duration_seconds))
| fields event_id, numeric_value, duration_seconds, y_component
| limit 3
```

**Explanation**: This query computes the y-component of a polar coordinate transformation using the formula `y = r * sin(θ)`, where `numeric_value` is the radius and `duration_seconds` is the angle in radians.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | Y\_COMPONENT |
| --------- | -------------- | ----------------- | ------------ |
| 101       | 5.0            | 0.0               | 0.0          |
| 102       | 3.0            | 1.5708            | 3.0          |
| 103       | 7.0            | 3.14159           | 0.0          |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`asin()`](asin), [`cos()`](cos), [`tan()`](tan), `pi()`
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
