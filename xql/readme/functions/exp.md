# exp

Use the `exp()` function to calculate the value of Euler's number `e` raised to the power of a numeric value.

## Syntax

```sql
exp(<number>)
```

## Parameters

| Name     | Type           | Required | Description                                                                            |
| -------- | -------------- | -------- | -------------------------------------------------------------------------------------- |
| `number` | integer, float | Yes      | The exponent to which `e` (approximately 2.71828) is raised. Any real number is valid. |

## Returns

**Type**: float

**Description**: The `exp()` function returns `e` raised to the power of the input value (e^x). If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `exp()` function accepts any real number as input.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Identity Value**: `exp(0)` always returns `1.0`, since `e^0 = 1`.
* **Inverse Relationship**: The `exp()` function is the inverse of the natural logarithm `ln()`. That is, `exp(ln(x)) = x` for `x > 0`.
* **Overflow**: For very large positive input values, the result may overflow to infinity.
* **Underflow**: For very large negative input values, the result approaches `0.0`.
* **Common Use Cases**: This function is typically used within the `alter` stage for exponential growth/decay modeling, probability calculations, and scientific computations.

## Examples

### Example 1: Calculate exponential of literal values

**Goal**: Calculate `e` raised to specific powers to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = exp(0), result2 = exp(1), result3 = exp(-1)
| fields result1, result2, result3
```

**Explanation**: You use `exp()` on three different literal values. `exp(0)` returns `1.0`, `exp(1)` returns approximately `2.71828` (the value of `e`), and `exp(-1)` returns approximately `0.36788` (1/e).

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 1.0     | 2.71828 | 0.36788 |

### Example 2: Calculate exponential from a field value

**Goal**: Calculate the exponential of values stored in a dataset field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter exp_result = exp(duration_seconds)
| fields event_id, duration_seconds, exp_result
| limit 3
```

**Explanation**: This query computes `e` raised to the power of each value in the `duration_seconds` field using `exp()` in the `alter` stage. No filtering is needed since `exp()` accepts any real number.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | EXP\_RESULT |
| --------- | ----------------- | ----------- |
| 101       | 0.0               | 1.0         |
| 102       | 1.0               | 2.71828     |
| 103       | 2.0               | 7.38906     |

### Example 3: Verify inverse relationship with ln

**Goal**: Demonstrate that `exp()` and `ln()` are inverse functions by applying both sequentially.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value > 0
| alter ln_val = ln(numeric_value)
| alter exp_ln_val = exp(ln_val)
| fields event_id, numeric_value, ln_val, exp_ln_val
| limit 3
```

**Explanation**: This query first computes the natural logarithm of `numeric_value`, then applies `exp()` to the result. The final value `exp_ln_val` should match the original `numeric_value`, confirming the inverse relationship `exp(ln(x)) = x`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | LN\_VAL | EXP\_LN\_VAL |
| --------- | -------------- | ------- | ------------ |
| 101       | 5.0            | 1.60944 | 5.0          |
| 102       | 10.0           | 2.30259 | 10.0         |
| 103       | 100.0          | 4.60517 | 100.0        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`ln()`](ln), [`log()`](log), [`pow()`](pow)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
