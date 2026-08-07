# power

Use the `power()` function to calculate the value of a number raised to the power of another number. This function is an alias for `pow()`.

## Syntax

```sql
power(<base>, <exponent>)
```

## Parameters

| Name       | Type           | Required | Description                               |
| ---------- | -------------- | -------- | ----------------------------------------- |
| `base`     | integer, float | Yes      | The base number to be raised.             |
| `exponent` | integer, float | Yes      | The exponent to which the base is raised. |

## Returns

**Type**: float

**Description**: The `power()` function returns the numerical result of the base raised to the power of the exponent. If either input is `null`, the function returns `null`.

## Usage notes

* **Input type**: XQL doesn't support NaN or infinite values as input and these value types also can not be returned.
* **Alias**: `power()` is functionally identical to `pow()`. Both functions can be used interchangeably.
* **Valid Input Range**: The function accepts any numeric values for both base and exponent, including negative numbers and zero.
* **Null Handling**: If either input expression is `null`, the function returns `null`.
* **Special Cases**: `power(x, 0)` returns `1.0` for any non-zero `x`. `power(0, 0)` returns `1.0`. `power(0, n)` returns `0.0` for `n > 0`.
* **Negative Base**: When the base is negative and the exponent is not an integer, the result may be `NaN`.
* **Common Use Cases**: This function is typically used within the `alter` stage for exponential calculations, area/volume computations, and scientific formulas.

## Examples

### Example 1: Calculate power of literal values

**Goal**: Calculate specific power operations to verify known mathematical results.

**XQL code**:

```sql
dataset = xdr_data
| limit 1
| alter result1 = power(2, 10), result2 = power(3, 3), result3 = power(10, -2)
| fields result1, result2, result3
```

**Explanation**: `power(2, 10)` returns `1024` (2^10), `power(3, 3)` returns `27` (3^3), and `power(10, -2)` returns `0.01` (10^-2 = 1/100).

**Output**:

| RESULT1 | RESULT2 | RESULT3 |
| ------- | ------- | ------- |
| 1024    | 27      | 0.01    |

### Example 2: Square field values using power

**Goal**: Calculate the square of values stored in a dataset field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter squared_value = power(duration_seconds, 2)
| fields event_id, duration_seconds, squared_value
| limit 3
```

**Explanation**: This query squares each value in the `duration_seconds` field using `power()` with an exponent of 2. For example, 1.5 squared is 2.25.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | SQUARED\_VALUE |
| --------- | ----------------- | -------------- |
| 101       | 1.5               | 2.25           |
| 102       | 0.8               | 0.64           |
| 103       | 10.2              | 104.04         |

### Example 3: Calculate square root using power with fractional exponent

**Goal**: Demonstrate that `power(x, 0.5)` is equivalent to the square root.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter numeric_value > 0
| alter sqrt_via_power = power(numeric_value, 0.5)
| alter sqrt_direct = sqrt(numeric_value)
| fields event_id, numeric_value, sqrt_via_power, sqrt_direct
| limit 3
```

**Explanation**: This query demonstrates that raising a number to the power of 0.5 is equivalent to taking its square root. Both `power(x, 0.5)` and `sqrt(x)` produce the same result.

**Output**:

| EVENT\_ID | NUMERIC\_VALUE | SQRT\_VIA\_POWER | SQRT\_DIRECT |
| --------- | -------------- | ---------------- | ------------ |
| 101       | 4.0            | 2.0              | 2.0          |
| 102       | 9.0            | 3.0              | 3.0          |
| 103       | 16.0           | 4.0              | 4.0          |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`pow()`](pow), [`sqrt()`](sqrt), [`exp()`](exp), [`multiply()`](multiply)
* **Datasets**: [`xdr_data`](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
