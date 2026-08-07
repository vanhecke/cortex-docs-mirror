# div

Use the `div()` function to perform integer division of two numeric values, returning the quotient without the remainder.

## Syntax

```sql
div(<dividend>, <divisor>)
```

## Parameters

| Name       | Type           | Required | Description                                              |
| ---------- | -------------- | -------- | -------------------------------------------------------- |
| `dividend` | integer, float | Yes      | The number to be divided (numerator).                    |
| `divisor`  | integer, float | Yes      | The number to divide by (denominator). Must not be zero. |

## Returns

**Type**: integer

**Description**: The `div()` function returns the integer quotient of the division, truncating any fractional part. If either input is `null` or the divisor is zero, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Integer Division**: Unlike the `divide()` function which returns a float, `div()` performs integer (truncated) division and returns only the whole number part of the quotient.
* **Division by Zero**: If the `divisor` is zero, the function returns `null` or raises an error.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Truncation Direction**: The result is truncated toward zero. For example, `div(7, 2)` returns `3` and `div(-7, 2)` returns `-3`.
* **Common Use Cases**: This function is typically used within the `alter` stage for bucketing values, calculating whole units, and performing modular arithmetic in combination with `mod()`.

## Examples

### Example 1: Integer division of literal values

**Goal**: Perform integer division on specific numeric literals to verify the truncation behavior.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = div(10, 3), result2 = div(7, 2), result3 = div(-7, 2)
| fields result1, result2, result3
```

**Explanation**: `div(10, 3)` returns `3` (10 ÷ 3 = 3 remainder 1), `div(7, 2)` returns `3` (7 ÷ 2 = 3 remainder 1), and `div(-7, 2)` returns `-3` (truncated toward zero).

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 3       | 3       | -3      |

### Example 2: Integer division from field values

**Goal**: Use integer division to calculate how many complete hours are in a duration measured in seconds.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter complete_hours = div(to_integer(multiply(duration_seconds, 3600)), 3600)
| fields event_id, duration_seconds, complete_hours
| limit 3
```

**Explanation**: This query converts `duration_seconds` to a larger value and then uses `div()` to find the number of complete hours, discarding any fractional hour.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | COMPLETE\_HOURS |
| --------- | ----------------- | --------------- |
| 101       | 7200.5            | 7200            |
| 102       | 3661.0            | 3661            |
| 103       | 1800.0            | 1800            |

### Example 3: Combine div with mod for quotient and remainder

**Goal**: Use `div()` and `mod()` together to decompose a value into its quotient and remainder.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter quotient = div(event_id, 10)
| alter remainder = mod(event_id, 10)
| fields event_id, quotient, remainder
| limit 3
```

**Explanation**: This query decomposes `event_id` into its quotient and remainder when divided by 10. For example, event\_id 101 gives quotient 10 and remainder 1, since 101 = 10 × 10 + 1.

**Output**:

| EVENT\_ID | QUOTIENT | REMAINDER |
| --------- | -------- | --------- |
| 101       | 10       | 1         |
| 102       | 10       | 2         |
| 103       | 10       | 3         |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`divide()`](divide), [`mod()`](mod), [`multiply()`](multiply), [`trunc()`](trunc)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
