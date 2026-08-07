# bitwise\_sright

Use the `bitwise_sright()` function to perform a bitwise right shift operation on an integer value by a specified number of positions.

## Syntax

```sql
bitwise_sright (<left_clause>, <right_clause>)
```

## Parameters

| Name           | Type    | Required | Description                                                    |
| -------------- | ------- | -------- | -------------------------------------------------------------- |
| `left_clause`  | integer | Yes      | The integer value or field whose bits are to be shifted right. |
| `right_clause` | integer | Yes      | The number of bit positions to shift right.                    |

## Returns

The `bitwise_sright()` function returns an integer representing the result of shifting the bits of the first parameter to the right by the number of positions specified in the second parameter.

## Usage notes

* The function performs a bitwise right shift (`>>`) operation, moving each bit of the value to the right by the specified number of positions. Bits shifted beyond the least significant position are discarded.
* Each right shift by 1 position effectively performs integer division by 2. Shifting right by `n` positions divides the value by 2^n (discarding any remainder).
* Both parameters must be integers. Passing a string value will result in a validation error.
* This function is useful for extracting values from specific bit positions within a packed integer, or for dividing by powers of two.
* The function is typically used within the `alter` or `filter` stages to create computed fields or filter events based on bitwise conditions.

## Examples

### Example 1: Shift a field value right by 1 position

**Goal**: Halve the value of the `event_type` field by shifting its bits one position to the right.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter halved_type = bitwise_sright(event_type, 1) 
| fields event_id, event_type, halved_type 
| limit 3
```

**Explanation**: This query shifts the bits of `event_type` one position to the right, effectively performing integer division by 2. For a value of 7 (binary `111`), the result is 3 (binary `11`).

**Output**:

| event\_id | event\_type | halved\_type |
| --------- | ----------- | ------------ |
| 101       | 7           | 3            |
| 102       | 10          | 5            |
| 103       | 4           | 2            |

### Example 2: Extract the upper byte from a 16-bit value

**Goal**: Extract the upper 8 bits from a 16-bit integer field by shifting right 8 positions.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter upper_byte = bitwise_sright(action_status, 8) 
| fields event_id, action_status, upper_byte 
| limit 3
```

**Explanation**: This query shifts `action_status` right by 8 positions, extracting the upper byte. For a value of 512 (binary `0000001000000000`), the result is 2. For 1024, the result is 4.

**Output**:

| event\_id | action\_status | upper\_byte |
| --------- | -------------- | ----------- |
| 101       | 512            | 2           |
| 102       | 1024           | 4           |
| 103       | 256            | 1           |

### Example 3: Check a specific bit by shifting and masking

**Goal**: Determine whether bit 4 is set in the `event_type` field by shifting right 4 positions and checking the least significant bit with `bitwise_and()`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter bit4_value = bitwise_and(bitwise_sright(event_type, 4), 1) 
| fields event_id, event_type, bit4_value 
| limit 3
```

**Explanation**: This query first shifts `event_type` right by 4 positions, then uses `bitwise_and()` with 1 to isolate the least significant bit. If bit 4 was set in the original value, the result is 1; otherwise, it is 0. For a value of 16 (binary `10000`), the result is 1.

**Output**:

| event\_id | event\_type | bit4\_value |
| --------- | ----------- | ----------- |
| 101       | 16          | 1           |
| 102       | 7           | 0           |
| 103       | 31          | 1           |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`bitwise_sleft`](bitwise_sleft), [`bitwise_and`](bitwise_and), [`bitwise_or`](bitwise_or), [`bitwise_xor`](bitwise_xor), [`to_integer`](to_integer)
