# ln

Use the `ln()` function to calculate the natural logarithm (base `e`) of a numeric value.

## Syntax

```sql
ln(<number>)
```

## Parameters

| Name     | Type           | Required | Description                                                                                       |
| -------- | -------------- | -------- | ------------------------------------------------------------------------------------------------- |
| `number` | integer, float | Yes      | The numeric value for which to calculate the natural logarithm. The value must be greater than 0. |

## Returns

**Type**: float

**Description**: The `ln()` function returns the natural logarithm (base `e`) of the input value. If the input is `null`, zero, or negative, the function returns `null` or `NaN`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The input `number` must be strictly greater than 0. The natural logarithm is undefined for zero and negative numbers.
* **Zero Input**: `ln(0)` returns negative infinity or `null`.
* **Negative Input**: `ln(x)` for `x < 0` returns `NaN` or `null`.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Identity Value**: `ln(1)` always returns `0.0`, and `ln(e)` returns `1.0`.
* **Inverse Relationship**: The `ln()` function is the inverse of `exp()`. That is, `ln(exp(x)) = x` and `exp(ln(x)) = x` for `x > 0`.
* **Common Use Cases**: This function is typically used within the `alter` stage for logarithmic scaling, entropy calculations, growth rate analysis, and data normalization.

## Examples

### Example 1: Calculate natural logarithm of literal values

**Goal**: Calculate the natural logarithm for specific numeric literals to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = ln(1), result2 = ln(exp(1)), result3 = ln(10)
| fields result1, result2, result3
```

**Explanation**: `ln(1)` returns `0.0` (since `e^0 = 1`), `ln(e)` returns `1.0` (computed via `ln(exp(1))`), and `ln(10)` returns approximately `2.30259`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 0.0     | 1.0     | 2.30259 |

### Example 2: Calculate natural logarithm from a field value

**Goal**: Calculate the natural logarithm of values stored in a dataset field, filtering out non-positive values.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value > 0
| alter ln_result = ln(numeric_value)
| fields event_id, numeric_value, ln_result
| limit 3
```

**Explanation**: This query first filters the dataset to ensure `numeric_value` contains only positive values, then computes the natural logarithm for each value using `ln()` in the `alter` stage.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | LN\_RESULT |
| --------- | -------------- | ---------- |
| 101       | 1.0            | 0.0        |
| 102       | 10.0           | 2.30259    |
| 103       | 100.0          | 4.60517    |

### Example 3: Use natural logarithm for logarithmic scaling

**Goal**: Apply logarithmic scaling to large numeric values to compress the range for analysis.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id > 0
| alter log_scale_id = ln(event_id)
| fields event_id, log_scale_id
| limit 3
```

**Explanation**: This query applies `ln()` to the `event_id` field to create a logarithmically scaled version. This is useful for visualizing or analyzing data with a wide range of values.

**Output**:

| EVENT\_ID | LOG\_SCALE\_ID |
| --------- | -------------- |
| 101       | 4.61512        |
| 102       | 4.62497        |
| 103       | 4.63473        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`exp()`](exp), [`log()`](log), [`log10()`](log10)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
