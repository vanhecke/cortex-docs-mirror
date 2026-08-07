# cbrt

Use the `cbrt()` function to calculate the cube root of a numeric value.

## Syntax

```sql
cbrt(<number>)
```

## Parameters

| Name     | Type           | Required | Description                                                                                                   |
| -------- | -------------- | -------- | ------------------------------------------------------------------------------------------------------------- |
| `number` | integer, float | Yes      | The numeric value for which to calculate the cube root. Any real number is valid, including negative numbers. |

## Returns

**Type**: float

**Description**: The `cbrt()` function returns the cube root of the input value. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `cbrt()` function accepts any real number, including negative numbers and zero.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Negative Numbers**: Unlike square root (`sqrt()`), the cube root of a negative number is a valid real number. For example, `cbrt(-8)` returns `-2.0`.
* **Identity Values**: `cbrt(0)` returns `0.0`, `cbrt(1)` returns `1.0`, and `cbrt(-1)` returns `-1.0`.
* **Common Use Cases**: This function is typically used within the `alter` stage for mathematical transformations, volume calculations, and data normalization.

## Examples

### Example 1: Calculate cube root of literal values

**Goal**: Calculate the cube root for specific numeric literals to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = cbrt(8), result2 = cbrt(27), result3 = cbrt(-8)
| fields result1, result2, result3
```

**Explanation**: You use `cbrt()` on three different literal values. `cbrt(8)` returns `2.0`, `cbrt(27)` returns `3.0`, and `cbrt(-8)` returns `-2.0`, demonstrating that the function handles negative inputs correctly.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 2.0     | 3.0     | -2.0    |

### Example 2: Calculate cube root from a field value

**Goal**: Calculate the cube root of values stored in a dataset field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter cube_root_val = cbrt(numeric_value)
| fields event_id, numeric_value, cube_root_val
| limit 3
```

**Explanation**: This query computes the cube root for each value in the `numeric_value` field using `cbrt()` in the `alter` stage and stores the result in `cube_root_val`. No filtering is needed since `cbrt()` accepts any real number.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | CUBE\_ROOT\_VAL |
| --------- | -------------- | --------------- |
| 101       | 125.0          | 5.0             |
| 102       | -27.0          | -3.0            |
| 103       | 1000.0         | 10.0            |

### Example 3: Combine cube root with other operations

**Goal**: Use the cube root function as part of a larger mathematical expression.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter volume = multiply(numeric_value, multiply(numeric_value, numeric_value))
| alter side_length = cbrt(volume)
| fields event_id, numeric_value, volume, side_length
| limit 3
```

**Explanation**: This query first cubes the `numeric_value` to simulate a volume, then applies `cbrt()` to recover the original side length. The result in `side_length` should match the original `numeric_value`, demonstrating that `cbrt()` is the inverse of cubing.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | VOLUME | SIDE\_LENGTH |
| --------- | -------------- | ------ | ------------ |
| 101       | 3.0            | 27.0   | 3.0          |
| 102       | 5.0            | 125.0  | 5.0          |
| 103       | 10.0           | 1000.0 | 10.0         |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`sqrt()`](sqrt), [`pow()`](pow), [`multiply()`](multiply)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
