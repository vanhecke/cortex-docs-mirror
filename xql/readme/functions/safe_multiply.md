# safe\_multiply

Use the `safe_multiply()` function to perform multiplication of two numeric values with overflow protection. Unlike the standard `multiply()` function, `safe_multiply()` returns `null` instead of raising an error when the result overflows.

## Syntax

```sql
safe_multiply(<number1>, <number2>)
```

## Parameters

| Name      | Type           | Required | Description                           |
| --------- | -------------- | -------- | ------------------------------------- |
| `number1` | integer, float | Yes      | The first numeric value to multiply.  |
| `number2` | integer, float | Yes      | The second numeric value to multiply. |

## Returns

**Type**: integer or float (matches input types)

**Description**: The `safe_multiply()` function returns the product of the two input values. If the result would overflow the numeric type, the function returns `null` instead of raising an error. If either input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Overflow Protection**: The primary advantage of `safe_multiply()` over `multiply()` is that it returns `null` instead of raising an error when the result exceeds the maximum or minimum value of the numeric type.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Type Preservation**: When both inputs are integers, the result is an integer. When either input is a float, the result is a float.
* **Common Use Cases**: This function is used when working with potentially large numbers where overflow is a concern, such as multiplying large counters, calculating areas with large dimensions, or computing compound values.

## Examples

### Example 1: Safe multiplication of literal values

**Goal**: Perform safe multiplication on numeric literals, including cases that might overflow.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = safe_multiply(100, 200)
| alter result2 = safe_multiply(9223372036854775807, 2)
| fields result1, result2
```

**Explanation**: `safe_multiply(100, 200)` returns `20000` as expected. `safe_multiply(9223372036854775807, 2)` would overflow the maximum 64-bit integer value, so it returns `null` instead of raising an error.

**Output**:

| RESULT1 | RESULT2 |
| ------- | ------- |
| 20000   | null    |

### Example 2: Safe multiplication of field values

**Goal**: Safely multiply two numeric fields that might produce overflow.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter safe_product = safe_multiply(event_id, numeric_value)
| fields event_id, numeric_value, safe_product
| limit 3
```

**Explanation**: This query safely multiplies `event_id` and `numeric_value` for each record. If any combination would cause an overflow, the result is `null` rather than an error.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SAFE\_PRODUCT |
| --------- | -------------- | ------------- |
| 101       | 5.0            | 505.0         |
| 102       | 200.0          | 20400.0       |
| 103       | 50.0           | 5150.0        |

### Example 3: Use safe\_multiply with coalesce for fallback

**Goal**: Perform safe multiplication and provide a fallback value when the result is null due to overflow.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter safe_result = safe_multiply(event_id, numeric_value)
| alter final_result = coalesce(safe_result, -1)
| fields event_id, numeric_value, safe_result, final_result
| limit 3
```

**Explanation**: This query uses `safe_multiply()` to multiply two fields, then applies `coalesce()` to replace any `null` results (from overflow or null inputs) with `-1` as a sentinel value.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SAFE\_RESULT | FINAL\_RESULT |
| --------- | -------------- | ------------ | ------------- |
| 101       | 5.0            | 505.0        | 505.0         |
| 102       | 200.0          | 20400.0      | 20400.0       |
| 103       | 50.0           | 5150.0       | 5150.0        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`multiply()`](multiply), [`safe_add()`](safe_add), [`safe_divide()`](safe_divide), [`coalesce()`](coalesce)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
