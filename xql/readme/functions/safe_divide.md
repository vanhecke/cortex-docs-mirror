# safe\_divide

Use the `safe_divide()` function to perform division of two numeric values with error protection. Unlike the standard `divide()` function, `safe_divide()` returns `null` instead of raising an error when dividing by zero.

## Syntax

```sql
safe_divide(<dividend>, <divisor>)
```

## Parameters

| Name       | Type           | Required | Description                            |
| ---------- | -------------- | -------- | -------------------------------------- |
| `dividend` | integer, float | Yes      | The number to be divided (numerator).  |
| `divisor`  | integer, float | Yes      | The number to divide by (denominator). |

## Returns

**Type**: float

**Description**: The `safe_divide()` function returns the result of dividing the `dividend` by the `divisor`. If the `divisor` is zero, the function returns `null` instead of raising an error. If either input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Division by Zero Protection**: The primary advantage of `safe_divide()` over `divide()` is that it returns `null` instead of raising an error when the divisor is zero.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Return Type**: The result is always a float, even when both inputs are integers.
* **Common Use Cases**: This function is used when the divisor might be zero, such as calculating ratios, percentages, or averages where the denominator could be zero in some records.

## Examples

### Example 1: Safe division with zero divisor

**Goal**: Demonstrate that `safe_divide()` returns null instead of an error when dividing by zero.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = safe_divide(10, 2), result2 = safe_divide(10, 0), result3 = safe_divide(0, 5)
| fields result1, result2, result3
```

**Explanation**: `safe_divide(10, 2)` returns `5.0`. `safe_divide(10, 0)` returns `null` instead of raising a division-by-zero error. `safe_divide(0, 5)` returns `0.0`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 5.0     | null    | 0.0     |

### Example 2: Calculate safe ratios from field values

**Goal**: Calculate a ratio between two fields where the denominator might be zero.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter ratio = safe_divide(numeric_value, duration_seconds)
| fields event_id, numeric_value, duration_seconds, ratio
| limit 3
```

**Explanation**: This query safely divides `numeric_value` by `duration_seconds`. If `duration_seconds` is zero for any record, the result is `null` rather than an error, preventing query failure.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | RATIO    |
| --------- | -------------- | ----------------- | -------- |
| 101       | 100.0          | 1.5               | 66.66667 |
| 102       | 50.0           | 0.0               | null     |
| 103       | 200.0          | 10.2              | 19.60784 |

### Example 3: Use safe\_divide with coalesce for fallback

**Goal**: Calculate a safe ratio and provide a default value when division by zero occurs.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter safe_ratio = safe_divide(numeric_value, duration_seconds)
| alter final_ratio = coalesce(safe_ratio, 0)
| fields event_id, numeric_value, duration_seconds, safe_ratio, final_ratio
| limit 3
```

**Explanation**: This query uses `safe_divide()` to calculate a ratio, then applies `coalesce()` to replace any `null` results (from division by zero or null inputs) with `0` as a fallback value.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | SAFE\_RATIO | FINAL\_RATIO |
| --------- | -------------- | ----------------- | ----------- | ------------ |
| 101       | 100.0          | 1.5               | 66.66667    | 66.66667     |
| 102       | 50.0           | 0.0               | null        | 0            |
| 103       | 200.0          | 10.2              | 19.60784    | 19.60784     |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`divide()`](divide), [`safe_multiply()`](safe_multiply), [`safe_add()`](safe_add), [`coalesce()`](coalesce)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
