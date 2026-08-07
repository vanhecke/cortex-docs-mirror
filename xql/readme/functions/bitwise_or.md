# bitwise\_or

Use the `bitwise_or()` function to perform a bitwise OR operation between two integer values.

## Syntax

```sql
bitwise_or (<left_clause>, <right_clause>)
```

## Parameters

| Name           | Type    | Required | Description                                                          |
| -------------- | ------- | -------- | -------------------------------------------------------------------- |
| `left_clause`  | integer | Yes      | The first integer value or field on which to perform the bitwise OR. |
| `right_clause` | integer | Yes      | The second integer value or field to OR against the first value.     |

## Returns

The `bitwise_or()` function returns an integer representing the result of the bitwise OR operation between the two input parameters.

## Usage notes

* The function performs a bitwise OR (`|`) operation, comparing each bit of the first operand to the corresponding bit of the second operand. If either bit is 1, the corresponding result bit is set to 1; otherwise, it is set to 0.
* Both parameters must be integers. Passing a string value will result in a validation error.
* This function is commonly used to set specific bit flags or combine multiple bitmask values into a single field.
* The function supports hexadecimal integer values when used with `to_integer()` (for example, `to_integer("0x000b")`).
* The function is typically used within the `alter` or `filter` stages to create computed fields or filter events based on bitwise conditions.

## Examples

### Example 1: Set a specific bit flag in an integer field

**Goal**: Set bit 2 (value 4) in the `event_type` field, ensuring that flag is always present in the result.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter with_flag = bitwise_or(event_type, 4) 
| fields event_id, event_type, with_flag 
| limit 3
```

**Explanation**: This query performs a bitwise OR between `event_type` and 4 (binary `100`). If `event_type` is 3 (binary `011`), the result is 7 (binary `111`), ensuring bit 2 is set.

**Output**:

| event\_id | event\_type | with\_flag |
| --------- | ----------- | ---------- |
| 101       | 3           | 7          |
| 102       | 5           | 5          |
| 103       | 0           | 4          |

### Example 2: Combine two hexadecimal values and filter

**Goal**: Combine two hexadecimal values using bitwise OR and filter events where the result exceeds a threshold.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| filter bitwise_or(to_integer("0x0004"), to_integer("0x000b")) > 2 
| fields event_id, event_type 
| limit 3
```

**Explanation**: This query computes the bitwise OR of 0x0004 (decimal 4, binary `0100`) and 0x000b (decimal 11, binary `1011`), resulting in 15 (binary `1111`). Since 15 > 2, all events pass the filter.

**Output**:

| event\_id | event\_type |
| --------- | ----------- |
| 101       | 5           |
| 102       | 3           |
| 103       | 7           |

### Example 3: Merge flags from two separate fields

**Goal**: Merge the bit flags from two separate integer fields into a single combined field.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = xdr_data 
| alter combined_flags = bitwise_or(permission_read, permission_write) 
| fields event_id, permission_read, permission_write, combined_flags 
| limit 3
```

**Explanation**: This query combines the bit flags from `permission_read` and `permission_write`. For example, if `permission_read` is 1 (binary `01`) and `permission_write` is 2 (binary `10`), the result is 3 (binary `11`), indicating both permissions are active.

**Output**:

| event\_id | permission\_read | permission\_write | combined\_flags |
| --------- | ---------------- | ----------------- | --------------- |
| 101       | 1                | 2                 | 3               |
| 102       | 4                | 1                 | 5               |
| 103       | 0                | 8                 | 8               |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), [`filter`](../stages/filter), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`bitwise_and`](bitwise_and), [`bitwise_xor`](bitwise_xor), [`bitwise_sleft`](bitwise_sleft), [`bitwise_sright`](bitwise_sright), [`to_integer`](to_integer)
