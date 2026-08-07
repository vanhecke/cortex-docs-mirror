# safe\_add

Use the `safe_add()` function to perform addition of two numeric values with overflow protection. Unlike the standard `add()` function, `safe_add()` returns `null` instead of raising an error when the result overflows.

## Syntax

```sql
safe_add(<number1>, <number2>)
```

## Parameters

| Name      | Type           | Required | Description                      |
| --------- | -------------- | -------- | -------------------------------- |
| `number1` | integer, float | Yes      | The first numeric value to add.  |
| `number2` | integer, float | Yes      | The second numeric value to add. |

## Returns

**Type**: integer or float (matches input types)

**Description**: The `safe_add()` function returns the sum of the two input values. If the result would overflow the numeric type, the function returns `null` instead of raising an error. If either input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Overflow Protection**: The primary advantage of `safe_add()` over `add()` is that it returns `null` instead of raising an error when the result exceeds the maximum or minimum value of the numeric type.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Type Preservation**: When both inputs are integers, the result is an integer. When either input is a float, the result is a float.
* **Common Use Cases**: This function is used when working with potentially large numbers where overflow is a concern, such as summing large counters, byte counts, or accumulated metrics.

## Examples

### Example 1: Safe addition of literal values

**Goal**: Perform safe addition on numeric literals, including cases that might overflow.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = safe_add(100, 200)
| alter result2 = safe_add(9223372036854775807, 1)
| fields result1, result2
```

**Explanation**: `safe_add(100, 200)` returns `300` as expected. `safe_add(9223372036854775807, 1)` would overflow the maximum 64-bit integer value, so it returns `null` instead of raising an error.

**Output**:

| RESULT1 | RESULT2 |
| ------- | ------- |
| 300     | null    |

### Example 2: Safe addition of field values

**Goal**: Safely add two numeric fields that might produce overflow.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter safe_sum = safe_add(event_id, numeric_value)
| fields event_id, numeric_value, safe_sum
| limit 3
```

**Explanation**: This query safely adds `event_id` and `numeric_value` for each record. If any combination would cause an overflow, the result is `null` rather than an error.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SAFE\_SUM |
| --------- | -------------- | --------- |
| 101       | 5.0            | 106.0     |
| 102       | 200.0          | 302.0     |
| 103       | 50.0           | 153.0     |

### Example 3: Use safe\_add with coalesce for fallback

**Goal**: Perform safe addition and provide a fallback value when the result is null due to overflow.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter safe_result = safe_add(event_id, numeric_value)
| alter final_result = coalesce(safe_result, 0)
| fields event_id, numeric_value, safe_result, final_result
| limit 3
```

**Explanation**: This query uses `safe_add()` to add two fields, then applies `coalesce()` to replace any `null` results (from overflow or null inputs) with `0` as a fallback value.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SAFE\_RESULT | FINAL\_RESULT |
| --------- | -------------- | ------------ | ------------- |
| 101       | 5.0            | 106.0        | 106.0         |
| 102       | 200.0          | 302.0        | 302.0         |
| 103       | 50.0           | 153.0        | 153.0         |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`add()`](add), [`safe_subtract()`](safe_subtract), [`safe_multiply()`](safe_multiply), [`coalesce()`](coalesce)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
