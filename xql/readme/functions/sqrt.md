# sqrt

Use the `sqrt()` function to calculate the square root of a numeric value.

## Syntax

```sql
sqrt(<number>)
```

## Parameters

| Name     | Type           | Required | Description                                                                                             |
| -------- | -------------- | -------- | ------------------------------------------------------------------------------------------------------- |
| `number` | integer, float | Yes      | The numeric value for which to calculate the square root. The value must be greater than or equal to 0. |

## Returns

**Type**: float

**Description**: The `sqrt()` function returns the non-negative square root of the input value. If the input is `null` or negative, the function returns `null` or `NaN`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The input `number` must be greater than or equal to 0. The square root of a negative number is not a real number.
* **Negative Input**: If the input is negative, the function returns `NaN` or `null`.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Identity Values**: `sqrt(0)` returns `0.0`, `sqrt(1)` returns `1.0`.
* **Perfect Squares**: For perfect squares (for example, 4, 9, 16, 25), the result is an exact integer value represented as a float.
* **Relationship to power()**: `sqrt(x)` is equivalent to `power(x, 0.5)`.
* **Common Use Cases**: This function is typically used within the `alter` stage for distance calculations, standard deviation computations, normalization, and geometric formulas.

## Examples

### Example 1: Calculate square root of literal values

**Goal**: Calculate the square root for specific numeric literals to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = sqrt(4), result2 = sqrt(9), result3 = sqrt(2)
| fields result1, result2, result3
```

**Explanation**: `sqrt(4)` returns `2.0`, `sqrt(9)` returns `3.0`, and `sqrt(2)` returns approximately `1.41421`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 2.0     | 3.0     | 1.41421 |

### Example 2: Calculate square root from a field value

**Goal**: Calculate the square root of values stored in a dataset field, filtering out negative values.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value >= 0
| alter sqrt_result = sqrt(numeric_value)
| fields event_id, numeric_value, sqrt_result
| limit 3
```

**Explanation**: This query first filters the dataset to ensure `numeric_value` contains only non-negative values, then computes the square root for each value using `sqrt()` in the `alter` stage.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SQRT\_RESULT |
| --------- | -------------- | ------------ |
| 101       | 4.0            | 2.0          |
| 102       | 100.0          | 10.0         |
| 103       | 25.0           | 5.0          |

### Example 3: Calculate Euclidean distance using sqrt

**Goal**: Manually calculate the Euclidean distance between two 2D points using `sqrt()` and arithmetic functions.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter dx = subtract(numeric_value, 10)
| alter dy = subtract(duration_seconds, 5)
| alter distance = sqrt(add(multiply(dx, dx), multiply(dy, dy)))
| fields event_id, numeric_value, duration_seconds, distance
| limit 3
```

**Explanation**: This query calculates the Euclidean distance from each point `(numeric_value, duration_seconds)` to the reference point `(10, 5)` using the formula `sqrt((x2-x1)� + (y2-y1)�)`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | DISTANCE |
| --------- | -------------- | ----------------- | -------- |
| 101       | 4.0            | 1.5               | 7.28011  |
| 102       | 13.0           | 5.0               | 3.0      |
| 103       | 10.0           | 10.2              | 5.2      |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`power()`](power), [`cbrt()`](cbrt), [`euclidean_distance()`](euclidean_distance), [`multiply()`](multiply)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
