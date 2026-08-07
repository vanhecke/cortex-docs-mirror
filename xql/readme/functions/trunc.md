# trunc

Use the `trunc()` function to truncate a numeric value to a specified number of decimal places by removing (not rounding) the extra digits.

## Syntax

```sql
trunc(<number> [, <decimal_places>])
```

## Parameters

| Name             | Type           | Required | Description                                                                                                                                  |
| ---------------- | -------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `number`         | integer, float | Yes      | The numeric value to truncate.                                                                                                               |
| `decimal_places` | integer        | No       | The number of decimal places to keep. Defaults to 0 (truncate to integer). Negative values truncate digits to the left of the decimal point. |

## Returns

**Type**: float or integer

**Description**: The `trunc()` function returns the input value truncated to the specified number of decimal places. Unlike `round()`, which rounds to the nearest value, `trunc()` simply removes digits beyond the specified precision. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Truncation vs. Rounding**: `trunc()` removes digits without rounding. For example, `trunc(2.789, 1)` returns `2.7`, not `2.8`.
* **Default Behavior**: When `decimal_places` is omitted, the function truncates to 0 decimal places (i.e., returns the integer part).
* **Negative Decimal Places**: A negative `decimal_places` value truncates digits to the left of the decimal point. For example, `trunc(1234, -2)` returns `1200`.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Direction**: Truncation is always toward zero. For positive numbers, this is equivalent to `floor()`. For negative numbers, this is equivalent to `ceil()` (rounding toward zero, not toward negative infinity).
* **Common Use Cases**: This function is typically used within the `alter` stage for precision control, data formatting, bucketing values, and removing unwanted decimal places.

## Examples

### Example 1: Truncate literal values to different precisions

**Goal**: Truncate a numeric literal to various decimal places to demonstrate the behavior.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter trunc0 = trunc(3.14159), trunc2 = trunc(3.14159, 2), trunc4 = trunc(3.14159, 4)
| fields trunc0, trunc2, trunc4
```

**Explanation**: `trunc(3.14159)` returns `3` (no decimal places), `trunc(3.14159, 2)` returns `3.14` (two decimal places), and `trunc(3.14159, 4)` returns `3.1415` (four decimal places). Note that the digits are removed, not rounded.

**Output**:

| TRUNC0 | TRUNC2 | TRUNC4 |
| ------ | ------ | ------ |
| 3      | 3.14   | 3.1415 |

### Example 2: Truncate field values to integer

**Goal**: Truncate floating-point field values to their integer part.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter truncated_duration = trunc(duration_seconds)
| fields event_id, duration_seconds, truncated_duration
| limit 3
```

**Explanation**: This query truncates each `duration_seconds` value to its integer part by removing the decimal portion. For example, `1.5` becomes `1` and `10.2` becomes `10`. Unlike `floor()`, `trunc()` rounds toward zero, so `-2.7` would become `-2` (not `-3`).

**Output**:

| EVENT\_ID | DURATION\_SECONDS | TRUNCATED\_DURATION |
| --------- | ----------------- | ------------------- |
| 101       | 1.5               | 1                   |
| 102       | 0.8               | 0                   |
| 103       | 10.2              | 10                  |

### Example 3: Truncate with negative decimal places

**Goal**: Truncate values to the nearest hundred using negative decimal places.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter truncated_id = trunc(event_id, -2)
| fields event_id, truncated_id
| limit 3
```

**Explanation**: Using `trunc()` with `-2` decimal places truncates the last two digits of the integer, effectively rounding down to the nearest hundred. For example, `101` becomes `100` and `215` becomes `200`.

**Output**:

| EVENT\_ID | TRUNCATED\_ID |
| --------- | ------------- |
| 101       | 100           |
| 102       | 100           |
| 103       | 100           |

### Example 4: Compare trunc with round and floor for negative numbers

**Goal**: Demonstrate the difference between `trunc()`, `round()`, and `floor()` for negative numbers.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter neg_val = multiply(duration_seconds, -1)
| alter trunc_val = trunc(neg_val)
| alter round_val = round(neg_val)
| alter floor_val = floor(neg_val)
| fields event_id, neg_val, trunc_val, round_val, floor_val
| limit 3
```

**Explanation**: For negative numbers, `trunc()` rounds toward zero (for example, `-1.5` becomes `-1`), `round()` rounds to the nearest integer (for example, `-1.5` becomes `-2`), and `floor()` rounds toward negative infinity (for example, `-1.5` becomes `-2`). This demonstrates the key behavioral difference between these functions.

**Output**:

| EVENT\_ID | NEG\_VAL | TRUNC\_VAL | ROUND\_VAL | FLOOR\_VAL |
| --------- | -------- | ---------- | ---------- | ---------- |
| 101       | -1.5     | -1         | -2         | -2         |
| 102       | -0.8     | 0          | -1         | -1         |
| 103       | -10.2    | -10        | -10        | -11        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`round()`](round), [`floor()`](floor), [`to_integer()`](to_integer)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
