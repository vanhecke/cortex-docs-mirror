# least

Use the `least()` function to return the smallest value from a list of expressions.

## Syntax

```sql
least(<expression1>, <expression2> [, ...])
```

## Parameters

| Name          | Type                              | Required | Description                                                                         |
| ------------- | --------------------------------- | -------- | ----------------------------------------------------------------------------------- |
| `expression1` | integer, float, string, timestamp | Yes      | The first value to compare.                                                         |
| `expression2` | integer, float, string, timestamp | Yes      | The second value to compare.                                                        |
| `...`         | integer, float, string, timestamp | No       | Additional values to compare. Any number of additional expressions can be provided. |

## Returns

**Type**: Same as input type

**Description**: The `least()` function returns the smallest value among all the provided expressions. If any input is `null`, the function may skip `null` values or return `null` depending on the implementation.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Multiple Arguments**: The function accepts two or more arguments and returns the minimum value among them.
* **Type Consistency**: All arguments should be of compatible types for meaningful comparison.
* **Null Handling**: If all inputs are `null`, the function returns `null`. If some inputs are `null`, the function typically returns the least non-null value.
* **String Comparison**: When comparing strings, the function uses lexicographic (alphabetical) ordering.
* **Relationship to greatest()**: The `least()` function is the counterpart of `greatest()`, which returns the largest value.
* **Common Use Cases**: This function is typically used within the `alter` stage for selecting the minimum value across multiple fields, implementing upper bounds (capping values), and data normalization.

## Examples

### Example 1: Find least among literal values

**Goal**: Find the smallest value from a set of numeric literals.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter min_val = least(10, 25, 5, 42, 18)
| fields min_val
```

**Explanation**: The `least()` function compares all five literal values and returns `5`, the smallest among them.

**Output**:

| MIN\_VAL |
| -------- |
| 5        |

### Example 2: Find least value across multiple fields

**Goal**: Find the smallest value among multiple numeric fields for each record.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter min_field = least(event_id, numeric_value, duration_seconds)
| fields event_id, numeric_value, duration_seconds, min_field
| limit 3
```

**Explanation**: This query compares the values of `event_id`, `numeric_value`, and `duration_seconds` for each record and returns the smallest value in `min_field`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | DURATION\_SECONDS | MIN\_FIELD |
| --------- | -------------- | ----------------- | ---------- |
| 101       | 5.0            | 1.5               | 1.5        |
| 102       | 200.0          | 0.8               | 0.8        |
| 103       | 50.0           | 10.2              | 10.2       |

### Example 3: Implement an upper cap using least

**Goal**: Cap a value at a maximum threshold by using `least()` as an upper clamp.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter capped_duration = least(duration_seconds, 5.0)
| fields event_id, duration_seconds, capped_duration
| limit 3
```

**Explanation**: This query ensures that `capped_duration` does not exceed `5.0` by returning the lesser of `duration_seconds` and `5.0`. Values above `5.0` are capped, while values below remain unchanged.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | CAPPED\_DURATION |
| --------- | ----------------- | ---------------- |
| 101       | 1.5               | 1.5              |
| 102       | 0.8               | 0.8              |
| 103       | 10.2              | 5.0              |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`greatest()`](greatest), `min_by()`, [`coalesce()`](coalesce)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
