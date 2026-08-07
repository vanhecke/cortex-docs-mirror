# cos

Use the `cos()` function to calculate the cosine of a numeric value specified in radians.

## Syntax

```sql
cos(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                       |
| -------------------- | -------------- | -------- | --------------------------------------------------------------------------------- |
| `numeric_expression` | integer, float | Yes      | The angle in radians for which to calculate the cosine. Any real number is valid. |

## Returns

**Type**: float

**Description**: The `cos()` function returns the cosine of the input angle. The resulting value is within the range \[-1, 1].

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `cos()` function accepts any real number as input. The input is interpreted as an angle in radians.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Degrees to Radians**: If your input is in degrees, convert it to radians first by multiplying by `PI() / 180`.
* **Periodicity**: The cosine function is periodic with period 2π, meaning `cos(x) = cos(x + 2π)`.
* **Key Values**: `cos(0)` returns `1.0`, `cos(π/2)` returns `0.0`, `cos(π)` returns `-1.0`.
* **Common Use Cases**: This function is typically used within the `alter` stage for trigonometric calculations, signal processing, coordinate transformations, and distance computations.

## Examples

### Example 1: Calculate cosine of literal values

**Goal**: Calculate the cosine for specific radian values to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = cos(0), result2 = cos(pi()), result3 = cos(divide(pi(), 2))
| fields result1, result2, result3
```

**Explanation**: You use `cos()` on three different radian values. `cos(0)` returns `1.0`, `cos(π)` returns `-1.0`, and `cos(π/2)` returns approximately `0.0` (a very small number close to zero due to floating-point precision).

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 1.0     | -1.0    | 0.0     |

### Example 2: Calculate cosine from a field value

**Goal**: Calculate the cosine of values stored in a dataset field, treating them as angles in radians.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter cos_val = cos(numeric_value)
| fields event_id, numeric_value, cos_val
| limit 3
```

**Explanation**: This query computes the cosine for each value in the `numeric_value` field and stores the result in `cos_val`. Since `cos()` accepts any real number, no filtering is needed.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | COS\_VAL |
| --------- | -------------- | -------- |
| 101       | 0.0            | 1.0      |
| 102       | 1.5708         | 0.0      |
| 103       | 3.14159        | -1.0     |

### Example 3: Use cosine in a distance calculation

**Goal**: Use the cosine function as part of a spherical distance calculation between two points.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter cos_angle = cos(duration_seconds)
| alter scaled_cos = multiply(cos_angle, numeric_value)
| fields event_id, duration_seconds, cos_angle, numeric_value, scaled_cos
| limit 3
```

**Explanation**: This query calculates the cosine of `duration_seconds` (treated as an angle in radians) and then multiplies the result by `numeric_value` to produce a scaled cosine value, which is a common pattern in coordinate transformations.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | COS\_ANGLE | NUMERIC\_VALUE | SCALED\_COS |
| --------- | ----------------- | ---------- | -------------- | ----------- |
| 101       | 0.0               | 1.0        | 5.0            | 5.0         |
| 102       | 1.5708            | 0.0        | 3.0            | 0.0         |
| 103       | 3.14159           | -1.0       | 7.0            | -7.0        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`acos()`](acos), [`sin()`](sin), [`tan()`](tan), `pi()`
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
