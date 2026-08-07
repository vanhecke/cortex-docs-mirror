# pow

Use the `pow()` function to calculate the value of a number raised to the power of another number.

## Syntax

```sql
pow (<base>, <exponent>)
```

## Parameters

| Name       | Type                   | Required | Description                               |
| ---------- | ---------------------- | -------- | ----------------------------------------- |
| `base`     | integer, float, string | Yes      | The base number to be raised.             |
| `exponent` | integer, float, string | Yes      | The exponent to which the base is raised. |

## Returns

The `pow()` function returns the numerical result of the base raised to the power of the exponent.

## Usage notes

* The function accepts numeric literals (for example, 2, 1.5), floating-point numbers, and integers as input.
* Input values can also be provided as strings representing numbers (for example, extracted from a data field), which the function will convert for calculation.
* The function supports negative numbers for both the base and the exponent.

## Examples

### Example 1: Literal base and literal integer exponent (calculating 1 MB and 1 GB)

**Goal**: Calculate common byte sizes (Megabytes and Gigabytes) using integer literals, where 1MB is 2^20 bytes and 1GB is 2^30 bytes.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter mega_bytes = pow(2, 20)
| alter giga_bytes = pow(2, 30)
| fields event_id, mega_bytes, giga_bytes
| limit 3
```

**Explanation**: This query creates two new fields, `mega_bytes` and `giga_bytes`, by raising the literal 2 to the powers of 20 and 30 respectively. The result, 1048576 for 1MB and 1073741824 for 1GB, is a constant numerical value for each record.

**Output**:

| EVENT\_ID | MEGA\_BYTES | GIGA\_BYTES |
| --------- | ----------- | ----------- |
| 101       | 1048576     | 1073741824  |
| 102       | 1048576     | 1073741824  |
| 103       | 1048576     | 1073741824  |

### Example 2: Field base and literal integer exponent

**Goal**: Use a floating-point field as the base for a power calculation to square the value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter duration_squared = pow(duration_seconds, 2)
| fields event_id, duration_seconds, duration_squared
| limit 3
```

**Explanation**: The `duration_seconds` field (for example, 1.5, 0.8, 10.2) is raised to the power of 2 (squared). For instance, 1.5 becomes 2.25, and 0.8 becomes 0.64, demonstrating the function's precision with floating-point numbers.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | DURATION\_SQUARED |
| --------- | ----------------- | ----------------- |
| 101       | 1.5               | 2.25              |
| 102       | 0.8               | 0.64              |
| 103       | 10.2              | 104.04            |

### Example 3: Field base from array and literal integer exponent

**Goal**: Use an element extracted from an array field as the base for a power calculation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter first_numeric_code = arrayindex(numeric_codes, 0)
| alter code_cubed = pow(first_numeric_code, 3)
| fields event_id, numeric_codes, first_numeric_code, code_cubed
| limit 3
```

**Explanation**: This query extracts the first element (index 0) from the `numeric_codes` array for each record. The query then raises this extracted integer to the power of 3 (cubed), storing the result in `code_cubed`.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | FIRST\_NUMERIC\_CODE | CODE\_CUBED |
| --------- | -------------------------- | -------------------- | ----------- |
| 101       | \[13, -47, 29, 82, -15]    | 13                   | 2197        |
| 102       | \[-21, 56, 13, -88, 42]    | -21                  | -9261       |
| 103       | \[90, -33, 7, 51, -62, 18] | 90                   | 729000      |

### Example 4: Literal base and negative integer exponent from array

**Goal**: Raise a literal base to the power of a negative exponent extracted from an array field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter second_numeric_code = arrayindex(numeric_codes, 1)
| alter base_powered_by_code = pow(10, second_numeric_code)
| fields event_id, numeric_codes, second_numeric_code, base_powered_by_code
| limit 3
```

**Explanation**: For event\_id 101, `second_numeric_code` is -47. The calculation becomes 10^-47, resulting in a very small floating-point number (scientific notation 1e-47). This illustrates how `pow()` correctly handles negative exponents, producing decimal results.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | SECOND\_NUMERIC\_CODE | BASE\_POWERED\_BY\_CODE |
| --------- | -------------------------- | --------------------- | ----------------------- |
| 101       | \[13, -47, 29, 82, -15]    | -47                   | 1e-47                   |
| 102       | \[-21, 56, 13, -88, 42]    | 56                    | 1e+56                   |
| 103       | \[90, -33, 7, 51, -62, 18] | -33                   | 1e-33                   |

### Example 5: Negative base and literal integer exponent

**Goal**: Calculate the power of a negative base number.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter pow_negative_base = pow(-5, 3)
| fields event_id, pow_negative_base
| limit 3
```

**Explanation**: This calculates -5 multiplied by itself three times (-5 _-5_ -5), resulting in -125. The result is consistently -125 across records as the inputs are literals.

**Output**:

| EVENT\_ID | POW\_NEGATIVE\_BASE |
| --------- | ------------------- |
| 101       | -125                |
| 102       | -125                |
| 103       | -125                |

### Example 6: Field base and zero exponent

**Goal**: Demonstrate the mathematical rule that any non-zero number raised to the power of zero equals one.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter zero_exponent_result = pow(event_id, 0)
| fields event_id, zero_exponent_result
| limit 3
```

**Explanation**: Regardless of the `event_id` value (as long as it's non-zero), `pow(<number>, 0)` will always return 1, following standard mathematical rules.

**Output**:

| EVENT\_ID | ZERO\_EXPONENT\_RESULT |
| --------- | ---------------------- |
| 101       | 1                      |
| 102       | 1                      |
| 103       | 1                      |

### Example 7: Extracting from JSON and applying pow

**Goal**: Extract a numeric value from JSON data and use it as the base for a power calculation.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter simple_json_data != null
| alter json_code_string = simple_json_data -> code
| alter json_numeric_value = to_number(json_code_string)
| alter code_to_power_of_two = pow(json_numeric_value, 2)
| fields event_id, simple_json_data, json_numeric_value, code_to_power_of_two
| limit 3
```

**Explanation**: This query first extracts the `code` value (for example, "200") from the `simple_json_data` field as a string. The query then converts this string to a number using `to_number()` and applies `pow()` with a literal exponent, storing the result in `code_to_power_of_two`.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA            | JSON\_NUMERIC\_VALUE | CODE\_TO\_POWER\_OF\_TWO |
| --------- | ----------------------------- | -------------------- | ------------------------ |
| 101       | {"status": "ok", "code": 200} | 200                  | 40000                    |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit), [`filter`](../stages/filter)
* **Functions**: [`arrayindex`](arrayindex), [`to_number`](to_number)
