# asin

Use the `asin()` function to calculate the principal value of the inverse sine (arcsine) of a numerical expression.

## Syntax

```sql
asin(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                                                        |
| -------------------- | -------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| `numeric_expression` | integer, float | Yes      | The numerical value for which to calculate the arcsine. The value must be within the range of -1 to 1 (inclusive). |

## Returns

**Type**: float

**Description**: The `asin()` function returns the principal value of the arcsine of the input in radians. The resulting value is within the range \[-π/2, π/2].

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The input `numeric_expression` must fall within the closed interval \[-1, 1].
* **Out of Range Behavior**: If the input is outside the range of -1 to 1, the function returns `NaN` (Not a Number) or `null`.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Radians to Degrees**: The result is provided in radians. To convert the result to degrees, multiply the return value by `180 / PI()`.
* **Common Use Cases**: This function is typically used within the `alter` stage for geometric calculations, spatial analysis, or normalizing data vectors.

## Examples

### Example 1: Calculate arcsine of literal values

**Goal**: Calculate the inverse sine for specific numerical literals to see the radian results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = asin(0), result2 = asin(1), result3 = asin(-1)
| fields result1, result2, result3
```

**Explanation**: You use `asin()` on three different literal values. `asin(0)` returns `0.0`, `asin(1)` returns approximately `1.5708` (π/2), and `asin(-1)` returns approximately `-1.5708` (-π/2).

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 0.0     | 1.5708  | -1.5708 |

### Example 2: Calculate arcsine from a field value

**Goal**: Calculate the arcsine of values stored in a specific field, ensuring they are within the valid mathematical range.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter duration_seconds >= -1 and duration_seconds <= 1
| alter arc_sin_val = asin(duration_seconds)
| fields event_id, duration_seconds, arc_sin_val
| limit 3
```

**Explanation**: This query first filters the dataset to ensure `duration_seconds` contains only values between -1 and 1, then computes the arcsine for each and stores it in `arc_sin_val`.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | ARC\_SIN\_VAL |
| --------- | ----------------- | ------------- |
| 101       | 0.5               | 0.5236        |
| 102       | -0.3              | -0.3047       |
| 103       | 1.0               | 1.5708        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`sin()`](sin), [`acos()`](acos), `atan()`
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
