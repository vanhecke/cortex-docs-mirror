# greatest

Use the `greatest()` function to return the largest value from a list of expressions.

## Syntax

```sql
greatest(<expression1>, <expression2> [, ...])
```

## Parameters

| Name          | Type                              | Required | Description                                                                         |
| ------------- | --------------------------------- | -------- | ----------------------------------------------------------------------------------- |
| `expression1` | integer, float, string, timestamp | Yes      | The first value to compare.                                                         |
| `expression2` | integer, float, string, timestamp | Yes      | The second value to compare.                                                        |
| `...`         | integer, float, string, timestamp | No       | Additional values to compare. Any number of additional expressions can be provided. |

## Returns

**Type**: Same as input type

**Description**: The `greatest()` function returns the largest value among all the provided expressions. If any input is `null`, the function may skip `null` values or return `null` depending on the implementation.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Multiple Arguments**: The function accepts two or more arguments and returns the maximum value among them.
* **Type Consistency**: All arguments should be of compatible types for meaningful comparison.
* **Null Handling**: If all inputs are `null`, the function returns `null`. If some inputs are `null`, the function typically returns the greatest non-null value.
* **String Comparison**: When comparing strings, the function uses lexicographic (alphabetical) ordering.
* **Relationship to least()**: The `greatest()` function is the counterpart of `least()`, which returns the smallest value.
* **Common Use Cases**: This function is typically used within the `alter` stage for selecting the maximum value across multiple fields, implementing upper bounds, and data normalization.

## Examples

### Example 1: Find greatest among literal values

**Goal**: Find the largest value from a set of numeric literals.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter max_val = greatest(10, 25, 5, 42, 18)
| fields max_val
```

**Explanation**: The `greatest()` function compares all five literal values and returns `42`, the largest among them.

**Output**:

| MAX\_VAL |
| -------- |
| 42       |

### Example 2: Find greatest value across multiple fields

**Goal**: Find the largest value among multiple numeric fields for each record.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter max_field = greatest(event_id, numeric_value, duration_seconds)
| fields event_id, numeric_value, duration_seconds, max_field
| limit 3
```

**Explanation**: This query compares the values of `event_id`, `numeric_value`, and `duration_seconds` for each record and returns the largest value in `max_field`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | MAX\_FIELD |
| --------- | -------------- | ----------------- | ---------- |
| 101       | 5.0            | 1.5               | 101        |
| 102       | 200.0          | 0.8               | 200.0      |
| 103       | 50.0           | 10.2              | 103        |

### Example 3: Implement an upper bound using greatest

**Goal**: Ensure a value is at least a minimum threshold by using `greatest()` as a lower clamp.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter clamped_duration = greatest(duration_seconds, 1.0)
| fields event_id, duration_seconds, clamped_duration
| limit 3
```

**Explanation**: This query ensures that `clamped_duration` is at least `1.0` by returning the greater of `duration_seconds` and `1.0`. Values below `1.0` are raised to `1.0`, while values above remain unchanged.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | CLAMPED\_DURATION |
| --------- | ----------------- | ----------------- |
| 101       | 1.5               | 1.5               |
| 102       | 0.8               | 1.0               |
| 103       | 10.2              | 10.2              |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`least()`](least), `max_by()`, [`coalesce()`](coalesce)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
