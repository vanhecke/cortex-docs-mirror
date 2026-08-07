# sign

Use the `sign()` function to determine the sign of a numeric value. The function returns -1, 0, or 1 depending on whether the input is negative, zero, or positive.

## Syntax

```sql
sign(<number>)
```

## Parameters

| Name     | Type           | Required | Description                                       |
| -------- | -------------- | -------- | ------------------------------------------------- |
| `number` | integer, float | Yes      | The numeric value whose sign is to be determined. |

## Returns

**Type**: integer

**Description**: The `sign()` function returns `-1` if the input is negative, `0` if the input is zero, and `1` if the input is positive. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `sign()` function accepts any real number.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Return Values**: The function always returns one of three values: `-1`, `0`, or `1`.
* **NaN Handling**: If the input is `NaN`, the behavior depends on the implementation and may return `null` or `NaN`.
* **Common Use Cases**: This function is typically used within the `alter` stage for direction detection, trend analysis, conditional logic based on value polarity, and data classification.

## Examples

### Example 1: Determine sign of literal values

**Goal**: Determine the sign of specific numeric literals.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter sign_pos = sign(42), sign_neg = sign(-17), sign_zero = sign(0)
| fields sign_pos, sign_neg, sign_zero
```

**Explanation**: `sign(42)` returns `1` (positive), `sign(-17)` returns `-1` (negative), and `sign(0)` returns `0` (zero).

**Output**:

| SIGN\_POS | SIGN\_NEG | SIGN\_ZERO |
| --------- | --------- | ---------- |
| 1         | -1        | 0          |

### Example 2: Classify field values by sign

**Goal**: Classify values in a dataset field as positive, negative, or zero.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter value_sign = sign(numeric_value)
| alter classification = if(value_sign = 1, "positive", value_sign = -1, "negative", "zero")
| fields event_id, numeric_value, value_sign, classification
| limit 4
```

**Explanation**: This query determines the sign of each `numeric_value` and maps it to a human-readable classification label using `if()`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | VALUE\_SIGN | CLASSIFICATION |
| --------- | -------------- | ----------- | -------------- |
| 101       | 5.0            | 1           | positive       |
| 102       | -200.0         | -1          | negative       |
| 103       | 0.0            | 0           | zero           |
| 104       | 50.0           | 1           | positive       |

### Example 3: Use sign for directional comparison

**Goal**: Determine the direction of change between two fields.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter change = subtract(numeric_value, duration_seconds)
| alter direction = sign(change)
| alter trend = if(direction = 1, "increasing", direction = -1, "decreasing", "unchanged")
| fields event_id, numeric_value, duration_seconds, change, trend
| limit 3
```

**Explanation**: This query calculates the difference between `numeric_value` and `duration_seconds`, then uses `sign()` to determine the direction of the change. The result is mapped to a trend label.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | CHANGE | TREND      |
| --------- | -------------- | ----------------- | ------ | ---------- |
| 101       | 5.0            | 1.5               | 3.5    | increasing |
| 102       | 0.8            | 200.0             | -199.2 | decreasing |
| 103       | 10.2           | 10.2              | 0.0    | unchanged  |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`if()`](if), [`subtract()`](subtract), [`safe_negate()`](safe_negate)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
