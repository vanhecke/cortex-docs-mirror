# bitwise\_sleft

Use the `bitwise_sleft()` function to perform a bitwise left shift operation on an integer value by a specified number of positions.

## Syntax

```sql
bitwise_sleft (<left_clause>, <right_clause>)
```

## Parameters

| Name           | Type    | Required | Description                                                   |
| -------------- | ------- | -------- | ------------------------------------------------------------- |
| `left_clause`  | integer | Yes      | The integer value or field whose bits are to be shifted left. |
| `right_clause` | integer | Yes      | The number of bit positions to shift left.                    |

## Returns

The `bitwise_sleft()` function returns an integer representing the result of shifting the bits of the first parameter to the left by the number of positions specified in the second parameter.

## Usage notes

* The function performs a bitwise left shift (`<<`) operation, moving each bit of the value to the left by the specified number of positions. New bits on the right are filled with 0.
* Each left shift by 1 position effectively multiplies the value by 2. Shifting left by `n` positions multiplies the value by 2^n.
* Both parameters must be integers. Passing a string value will result in a validation error.
* This function is useful for constructing bitmask values, scaling values by powers of two, or encoding data into specific bit positions.
* The function is typically used within the `alter` or `filter` stages to create computed fields or filter events based on bitwise conditions.

## Examples

### Example 1: Shift a field value left by 1 position

**Goal**: Double the value of the `event_type` field by shifting its bits one position to the left.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter doubled_type = bitwise_sleft(event_type, 1) 
| fields event_id, event_type, doubled_type 
| limit 3
```

**Explanation**: This query shifts the bits of `event_type` one position to the left, effectively multiplying by 2. For a value of 5 (binary `101`), the result is 10 (binary `1010`).

**Output**:

| event\_id | event\_type | doubled\_type |
| --------- | ----------- | ------------- |
| 101       | 5           | 10            |
| 102       | 3           | 6             |
| 103       | 7           | 14            |

### Example 2: Create a bitmask from a bit position

**Goal**: Convert a bit position number into its corresponding bitmask value by shifting 1 to the left.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter bitmask = bitwise_sleft(1, bit_position) 
| fields event_id, bit_position, bitmask 
| limit 3
```

**Explanation**: This query creates a bitmask by shifting the value 1 left by the number of positions specified in `bit_position`. For position 3, the result is 8 (binary `1000`). For position 0, the result is 1 (binary `1`).

**Output**:

| event\_id | bit\_position | bitmask |
| --------- | ------------- | ------- |
| 101       | 0             | 1       |
| 102       | 3             | 8       |
| 103       | 7             | 128     |

### Example 3: Scale a value by a power of two and filter

**Goal**: Multiply the `action_status` field by 256 (2^8) by shifting left 8 positions, then filter for results above a threshold.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter upper_byte = bitwise_sleft(action_status, 8) 
| filter upper_byte > 512 
| fields event_id, action_status, upper_byte 
| limit 3
```

**Explanation**: This query shifts `action_status` left by 8 positions, multiplying it by 256. For a value of 3, the result is 768. Only results greater than 512 pass the filter.

**Output**:

| event\_id | action\_status | upper\_byte |
| --------- | -------------- | ----------- |
| 102       | 3              | 768         |
| 103       | 10             | 2560        |
| 105       | 5              | 1280        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`bitwise_sright`](bitwise_sright), [`bitwise_and`](bitwise_and), [`bitwise_or`](bitwise_or), [`bitwise_xor`](bitwise_xor), [`to_integer`](to_integer)
