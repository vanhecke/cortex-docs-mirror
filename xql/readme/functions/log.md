# log

Use the `log()` function to calculate the logarithm of a numeric value with a specified base.

## Syntax

```sql
log(<number>, <base>)
```

## Parameters

| Name     | Type           | Required | Description                                                                               |
| -------- | -------------- | -------- | ----------------------------------------------------------------------------------------- |
| `number` | integer, float | Yes      | The numeric value for which to calculate the logarithm. The value must be greater than 0. |
| `base`   | integer, float | Yes      | The base of the logarithm. The value must be greater than 0 and not equal to 1.           |

## Returns

**Type**: float

**Description**: The `log()` function returns the logarithm of the input value with the specified base. If either input is `null`, or if `number` is ≤ 0, or if `base` is ≤ 0 or equal to 1, the function returns `null` or `NaN`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `number` must be strictly greater than 0. The `base` must be strictly greater than 0 and not equal to 1.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Special Cases**: `log(1, any_base)` always returns `0.0`. `log(base, base)` always returns `1.0`.
* **Relationship to Other Logarithms**: `log(x, e)` is equivalent to `ln(x)`. `log(x, 10)` is equivalent to `log10(x)`.
* **Change of Base**: The function implements the change of base formula internally: `log(x, b) = ln(x) / ln(b)`.
* **Common Use Cases**: This function is typically used within the `alter` stage for logarithmic calculations with custom bases, information theory computations (base 2), and scientific analysis.

## Examples

### Example 1: Calculate logarithm with different bases

**Goal**: Calculate logarithms with various bases to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter log_base2 = log(8, 2), log_base10 = log(1000, 10), log_base3 = log(27, 3)
| fields log_base2, log_base10, log_base3
```

**Explanation**: `log(8, 2)` returns `3.0` (since 2^3 = 8), `log(1000, 10)` returns `3.0` (since 10^3 = 1000), and `log(27, 3)` returns `3.0` (since 3^3 = 27).

**Output**:

| LOG\_BASE2 | LOG\_BASE10 | LOG\_BASE3 |
| ---------- | ----------- | ---------- |
| 3.0        | 3.0         | 3.0        |

### Example 2: Calculate logarithm from a field value

**Goal**: Calculate the base-2 logarithm of values stored in a dataset field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value > 0
| alter log2_result = log(numeric_value, 2)
| fields event_id, numeric_value, log2_result
| limit 3
```

**Explanation**: This query computes the base-2 logarithm for each positive value in the `numeric_value` field. Base-2 logarithms are commonly used in computing to determine the number of bits needed to represent a value.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | LOG2\_RESULT |
| --------- | -------------- | ------------ |
| 101       | 8.0            | 3.0          |
| 102       | 64.0           | 6.0          |
| 103       | 100.0          | 6.64386      |

### Example 3: Use logarithm for information entropy calculation

**Goal**: Calculate the information content (in bits) of event probabilities using base-2 logarithm.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter duration_seconds > 0 and duration_seconds < 1
| alter info_content = multiply(-1, log(duration_seconds, 2))
| fields event_id, duration_seconds, info_content
| limit 3
```

**Explanation**: This query calculates the information content in bits using the formula `-log2(p)`, where `p` is a probability-like value from `duration_seconds`. Higher information content indicates rarer events.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | INFO\_CONTENT |
| --------- | ----------------- | ------------- |
| 101       | 0.5               | 1.0           |
| 102       | 0.25              | 2.0           |
| 103       | 0.8               | 0.32193       |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`ln()`](ln), [`log10()`](log10), [`exp()`](exp), [`pow()`](pow)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
