# add

Use the `add()` function to calculate the sum of two numbers.

## Syntax

```sql
add (<value_1>, <value_2>)
```

## Parameters

| Name      | Type                   | Required | Description                        |
| --------- | ---------------------- | -------- | ---------------------------------- |
| `value_1` | integer, float, string | Yes      | The first numeric value or field.  |
| `value_2` | integer, float, string | Yes      | The second numeric value or field. |

## Returns

The `add()` function returns the mathematical sum of the two input parameters.

## Usage notes

* The function operates on numbers, supporting integer literals and floating-point numbers.
* The function also accepts field values that represent numbers, even if those values are stored as a string data type (for example, an integer stored as text).
* The function is typically used within the `alter` stage to create or modify fields based on calculated values.

## Examples

### Example 1: Adding an integer field and a literal integer

**Goal**: Add a fixed numerical value to an existing integer field (`event_id`) to create a new calculated field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter new_event_id = add(event_id, 100) // Adds 100 to the 'event_id' field 
| fields event_id, new_event_id 
| limit 3
```

**Explanation**: This query adds 100 to the `event_id` of each record, storing the result in a new field called `new_event_id`. For `event_id` 101, `new_event_id` becomes 201.

**Output**:

| event\_id | new\_event\_id |
| --------- | -------------- |
| 101       | 201            |
| 102       | 202            |
| 103       | 203            |

### Example 2: Adding two integer literal values

**Goal**: Perform addition directly on two static integer values to create a constant new field for each record.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter sum_of_literals = add(500, 25) // Adds two literal integer values 
| fields event_id, sum_of_literals 
| limit 3
```

**Explanation**: This query adds the literal integers 500 and 25, producing a constant `sum_of_literals` value of 525 for each record.

**Output**:

| event\_id | sum\_of\_literals |
| --------- | ----------------- |
| 101       | 525               |
| 102       | 525               |
| 103       | 525               |

### Example 3: Adding a floating-point field and a literal float

**Goal**: Operate on a floating-point number field and a literal floating-point value.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter increased_duration = add(duration_seconds, 0.5) // Adds 0.5 to 'duration_seconds' 
| fields event_id, duration_seconds, increased_duration 
| limit 3
```

**Explanation**: The `duration_seconds` field (a float) is increased by 0.5 for each record. For `event_id` 101 (duration 1.5), `increased_duration` becomes 2.0.

**Output**:

| event\_id | duration\_seconds | increased\_duration |
| --------- | ----------------- | ------------------- |
| 101       | 1.5               | 2.0                 |
| 102       | 0.8               | 1.3                 |
| 103       | 10.2              | 10.7                |

### Example 4: Adding an integer field and a negative literal

**Goal**: Handle a negative literal to effectively perform subtraction.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter adjusted_id = add(event_id, -10) // Subtracts 10 from 'event_id' 
| fields event_id, adjusted_id 
| limit 3
```

**Explanation**: This query subtracts 10 from the `event_id` of each record. For `event_id` 101, `adjusted_id` becomes 91.

**Output**:

| event\_id | adjusted\_id |
| --------- | ------------ |
| 101       | 91           |
| 102       | 92           |
| 103       | 93           |

### Example 5: Adding a number extracted as string and a literal

**Goal**: Use `add()` with a numeric value extracted from a JSON string field, which is first converted to a number.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter status_code_str = simple_json_data -> code // Extract 'code' as string 
| alter status_code_num = to_number(status_code_str) // Convert string to number 
| alter new_code_value = add(status_code_num, 50) // Add 50 to the numeric code 
| fields event_id, simple_json_data, new_code_value 
| limit 3
```

**Explanation**: For `event_id` 101, the `code` "200" is extracted as a string, converted to a number, and then 50 is added, resulting in `new_code_value` of 250. For `event_id` 102, `$.code` is NULL, so `new_code_value` will also be NULL.

**Output**:

| event\_id | simple\_json\_data                                   | new\_code\_value |
| --------- | ---------------------------------------------------- | ---------------- |
| 101       | "{"status": "ok", "code": 200} "                     | 250              |
| 102       | "{"status": "fail", "error": "access\_denied"} "     | NULL             |
| 103       | "{"connection\_id": "CONN-001", "protocol": "TCP"} " | NULL             |

### Example 6: Adding an element from an array field and a literal

**Goal**: Access an element from an array field and add a literal integer to it.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_numeric_code = arrayindex(numeric_codes, 0) // Get the first element of the array 
| alter increased_first_code = add(first_numeric_code, 10) // Add 10 to the first element 
| fields event_id, numeric_codes, increased_first_code 
| limit 3
```

**Explanation**: For `event_id` 101, the first element of `numeric_codes` (13) is extracted, and 10 is added to it, resulting in `increased_first_code` of 23.

**Output**:

| event\_id | numeric\_codes                | increased\_first\_code |
| --------- | ----------------------------- | ---------------------- |
| 101       | "\[13, -47, 29, 82, -15] "    | 23                     |
| 102       | "\[-21, 56, 13, -88, 42] "    | -11                    |
| 103       | "\[90, -33, 7, 51, -62, 18] " | 100                    |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), `timeframe`, [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`divide`](divide), [`multiply`](multiply), [`subtract`](subtract)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
