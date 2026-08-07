# csc

Use the `csc()` function to calculate the cosecant of a numeric value specified in radians. The cosecant is the reciprocal of the sine function.

## Syntax

```sql
csc(<numeric_expression>)
```

## Parameters

| Name                 | Type           | Required | Description                                                                                              |
| -------------------- | -------------- | -------- | -------------------------------------------------------------------------------------------------------- |
| `numeric_expression` | integer, float | Yes      | The angle in radians for which to calculate the cosecant. The value must not be zero or a multiple of π. |

## Returns

**Type**: float

**Description**: The `csc()` function returns the cosecant of the input angle, which is equivalent to `1 / sin(x)`. If the input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Valid Input Range**: The `csc()` function accepts any real number except values where `sin(x) = 0` (i.e., multiples of π, including zero), where the cosecant is undefined.
* **Undefined Values**: At `x = 0` and multiples of π, the function returns `infinity`, `NaN`, or `null` since the cosecant is undefined at these points.
* **Null Handling**: If the input expression is `null`, the function returns `null`.
* **Relationship**: `csc(x) = 1 / sin(x)`.
* **Result Range**: The result is always ≤ -1 or ≥ 1 (never between -1 and 1).
* **Common Use Cases**: This function is typically used within the `alter` stage for trigonometric calculations, wave analysis, and engineering computations.

## Examples

### Example 1: Calculate cosecant of literal values

**Goal**: Calculate the cosecant for specific radian values to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = csc(divide(pi(), 2)), result2 = csc(divide(pi(), 6)), result3 = csc(1)
| fields result1, result2, result3
```

**Explanation**: You use `csc()` on three different radian values. `csc(π/2)` returns `1.0` (since `sin(π/2) = 1`), `csc(π/6)` returns `2.0` (since `sin(π/6) = 0.5`), and `csc(1)` returns approximately `1.1884`.

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 1.0     | 2.0     | 1.18840 |

### Example 2: Calculate cosecant from a field value

**Goal**: Calculate the cosecant of values stored in a dataset field, filtering out values near zero.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value != 0
| alter csc_val = csc(numeric_value)
| fields event_id, numeric_value, csc_val
| limit 3
```

**Explanation**: This query filters out zero values (where cosecant is undefined), then computes the cosecant for each remaining value in the `numeric_value` field.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | CSC\_VAL |
| --------- | -------------- | -------- |
| 101       | 0.5            | 2.08583  |
| 102       | 1.0            | 1.18840  |
| 103       | 1.5708         | 1.0      |

### Example 3: Verify cosecant as reciprocal of sine

**Goal**: Demonstrate that `csc(x)` equals `1 / sin(x)` by computing both and comparing.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value != 0
| alter csc_val = csc(numeric_value)
| alter reciprocal_sin = divide(1, sin(numeric_value))
| fields event_id, numeric_value, csc_val, reciprocal_sin
| limit 3
```

**Explanation**: This query computes both `csc(numeric_value)` and `1 / sin(numeric_value)` to verify they produce the same result, confirming the mathematical identity `csc(x) = 1 / sin(x)`.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | CSC\_VAL | RECIPROCAL\_SIN |
| --------- | -------------- | -------- | --------------- |
| 101       | 0.5            | 2.08583  | 2.08583         |
| 102       | 1.0            | 1.18840  | 1.18840         |
| 103       | 1.5708         | 1.0      | 1.0             |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`sin()`](sin), [`sec()`](sec), `csch()`, [`cot()`](cot)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
