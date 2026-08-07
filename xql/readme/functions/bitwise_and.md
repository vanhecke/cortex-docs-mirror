# bitwise\_and

Use the `bitwise_and()` function to perform a bitwise AND operation between two integer values.

## Syntax

```sql
bitwise_and (<left_clause>, <right_clause>)
```

## Parameters

| Name           | Type    | Required | Description                                                           |
| -------------- | ------- | -------- | --------------------------------------------------------------------- |
| `left_clause`  | integer | Yes      | The first integer value or field on which to perform the bitwise AND. |
| `right_clause` | integer | Yes      | The second integer value or field to AND against the first value.     |

## Returns

The `bitwise_and()` function returns an integer representing the result of the bitwise AND operation between the two input parameters.

## Usage notes

* The function performs a bitwise AND (`&`) operation, comparing each bit of the first operand to the corresponding bit of the second operand. If both bits are 1, the corresponding result bit is set to 1; otherwise, it is set to 0.
* Both parameters must be integers. Passing a string value will result in a validation error.
* This function is commonly used to check whether specific bit flags are set in a bitmask field.
* The function supports hexadecimal integer values when used with `to_integer()` (for example, `to_integer("0x02")`).
* The function is typically used within the `alter` or `filter` stages to create computed fields or filter events based on bitwise conditions.

## Examples

### Example 1: Check a specific bit flag in an integer field

**Goal**: Use a bit mask to check whether a specific flag (bit 1, value 2) is set in the `xdm.case.score` field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter flag_check = bitwise_and(xdm.case.score, 2) 
| fields event_id, xdm.case.score, flag_check 
| limit 3
```

**Explanation**: This query performs a bitwise AND between `xdm.case.score` and 2 (binary `10`). If bit 1 is set in `xdm.case.score`, `flag_check` will be 2; otherwise, it will be 0.

**Output**:

| event\_id | xdm.case.score | flag\_check |
| --------- | -------------- | ----------- |
| 101       | 7              | 2           |
| 102       | 4              | 0           |
| 103       | 3              | 2           |

### Example 2: Filter events using a bitwise AND with hexadecimal values

**Goal**: Filter events where a specific bit flag (0x02) is set in the `xdm.case.score` field, using hexadecimal notation.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| filter bitwise_and(xdm.case.score, to_integer("0x02")) > 0
| fields event_id, xdm.case.score 
| limit 3
```

**Explanation**: This query filters for events where bit 1 (value 2) is set in `xdm.case.score`. The `to_integer("0x02")` converts the hexadecimal value 0x02 to the integer 2, which is used as the bitmask. The `bitwise_and()` result is either 2 (bit is set) or 0 (bit is not set). Only events where the result is greater than 0 pass the filter.

**Output**:

| event\_id | xdm.case.score |
| --------- | -------------- |
| 103       | 7              |
| 107       | 15             |
| 112       | 6              |

### Example 3: Mask out the lower 8 bits of an integer field

**Goal**: Extract the lower 8 bits from a numeric field using a bit mask of 255 (binary `11111111`).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter lower_byte = bitwise_and(action_status, 255) 
| fields event_id, action_status, lower_byte 
| limit 3
```

**Explanation**: This query isolates the lower 8 bits of the `action_status` field. For a value of 258 (binary `100000010`), the result is 2 (binary `00000010`).

**Output**:

| event\_id | action\_status | lower\_byte |
| --------- | -------------- | ----------- |
| 101       | 258            | 2           |
| 102       | 511            | 255         |
| 103       | 1024           | 0           |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`bitwise_or`](bitwise_or), [`bitwise_xor`](bitwise_xor), [`bitwise_sleft`](bitwise_sleft), [`bitwise_sright`](bitwise_sright), [`to_integer`](to_integer)
