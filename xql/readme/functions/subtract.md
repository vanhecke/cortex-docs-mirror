# subtract

Use the `subtract()` function to calculate the difference between two numbers by subtracting the second argument from the first.

## Syntax

```sql
subtract (<value_1>, <value_2>)
```

## Parameters

| Name      | Type                   | Required | Description                                                   |
| --------- | ---------------------- | -------- | ------------------------------------------------------------- |
| `value_1` | integer, float, string | Yes      | The first value (the minuend).                                |
| `value_2` | integer, float, string | Yes      | The second value (the subtrahend) to subtract from the first. |

## Returns

The `subtract()` function returns the numerical difference between the two input numbers.

## Usage notes

* The function accepts numeric literals, floating-point numbers, and integers.
* The function supports integers or numbers provided as a string type (for example, extracted from a data field).

## Examples

### Example 1: Subtracting an integer literal from an integer field

**Goal**: Subtract a specific integer literal from an existing integer field to create a new field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter reduced_event_id = subtract(event_id, 5)
| fields event_id, reduced_event_id
| limit 3
```

**Explanation**: This query calculates `reduced_event_id` by subtracting 5 from each `event_id`. For `event_id` 101, the result is 96.

**Output**:

| EVENT\_ID | REDUCED\_EVENT\_ID |
| --------- | ------------------ |
| 101       | 96                 |
| 102       | 97                 |
| 103       | 98                 |

### Example 2: Subtracting a floating-point literal from a floating-point field

**Goal**: Subtract a floating-point literal from an existing floating-point field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter adjusted_duration = subtract(duration_seconds, 0.75)
| fields event_id, duration_seconds, adjusted_duration
| limit 3
```

**Explanation**: Here, `duration_seconds` (which contains decimal values like 1.5 and 0.8) is decreased by 0.75, producing new floating-point values in `adjusted_duration`.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | ADJUSTED\_DURATION |
| --------- | ----------------- | ------------------ |
| 101       | 1.5               | 0.75               |
| 102       | 0.8               | 0.05               |
| 103       | 10.2              | 9.45               |

### Example 3: Subtracting one field from another field

**Goal**: Calculate the difference between values in two different fields.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter difference_in_ids = subtract(event_id, arrayindex(numeric_codes, 0))
| fields event_id, numeric_codes, difference_in_ids
| limit 3
```

**Explanation**: For `event_id` 101, `event_id` is 101 and the first element of `numeric_codes` (index 0) is 13, resulting in 101 - 13 = 88. For `event_id` 102, `event_id` is 102 and the first `numeric_code` is -21, so 102 - (-21) = 123.

**Output**:

| EVENT\_ID | NUMERIC\_CODES     | DIFFERENCE\_IN\_IDS |
| --------- | ------------------ | ------------------- |
| 101       | \[13, -47, 29,...] | 88                  |
| 102       | \[-21, 56, 13,...] | 123                 |
| 103       | \[90, -33, 7,...]  | 13                  |

### Example 4: Handling negative numbers (subtracting a negative literal)

**Goal**: Demonstrate the behavior when subtracting a negative number.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter negative_subtraction = subtract(duration_seconds, -2.0)
| fields event_id, duration_seconds, negative_subtraction
| limit 3
```

**Explanation**: For `event_id` 101, `duration_seconds` is 1.5. Subtracting -2.0 (which is equivalent to adding 2.0) results in 3.5. This aligns with the understanding that the `subtract()` function supports operations with negative numbers.

**Output**:

| EVENT\_ID | DURATION\_SECONDS | NEGATIVE\_SUBTRACTION |
| --------- | ----------------- | --------------------- |
| 101       | 1.5               | 3.5                   |
| 102       | 0.8               | 2.8                   |
| 103       | 10.2              | 12.2                  |

### Example 5: Subtracting a numeric value extracted from JSON data

**Goal**: Extract a number from a JSON field and perform a subtraction operation on it.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter simple_json_data != null
| alter json_code_number = to_number(simple_json_data -> "code")
| alter reduced_json_value = subtract(json_code_number, 50)
| fields event_id, simple_json_data, json_code_number, reduced_json_value
| limit 3
```

**Explanation**: This query extracts the `code` value (for example, "200") from the `simple_json_data` field as a string, converts it to a number using `to_number()`, and then subtracts 50 from it. Note that only `event_id` 101 has a "code" field in `simple_json_data` in the `sample_xql_raw` dataset.

**Output**:

| EVENT\_ID | SIMPLE\_JSON\_DATA            | JSON\_CODE\_NUMBER | REDUCED\_JSON\_VALUE |
| --------- | ----------------------------- | ------------------ | -------------------- |
| 101       | {"status": "ok", "code": 200} | 200                | 150                  |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`arrayindex`](arrayindex), [`to_number`](to_number)
