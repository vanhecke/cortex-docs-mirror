# arrayconcat

Use the `arrayconcat()` function to combine the elements of two or more specified arrays into a single, new array.

## Syntax

```sql
arrayconcat (<array1>, <array2>[, <array3>...])
```

## Parameters

| Name        | Type  | Required | Description                                             |
| ----------- | ----- | -------- | ------------------------------------------------------- |
| `array1`    | array | Yes      | The first array field whose elements will be combined.  |
| `array2`    | array | Yes      | The second array field whose elements will be combined. |
| `array3...` | array | No       | Additional array fields to be combined.                 |

## Returns

The `arrayconcat()` function returns a single, new array that contains all elements from the input arrays.

## Usage notes

* All the elements within the input array fields must be of the same data type.
* The function joins the input arrays sequentially. The elements from `array1` come first, followed by elements from `array2`, and so on, preserving their original order within each array.
* `arrayconcat()` simply joins the elements and does not inherently remove duplicate values. If you need a result array with only unique elements, apply the `arraydistinct()` function after `arrayconcat()`.
* This function is typically employed within the `alter` stage to create new fields or modify existing ones by combining array data.

## Examples

### Example 1: Concatenating two newly created arrays

**Goal**: Define two new arrays using `arraycreate()` and then concatenate them to form a single combined array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_part = arraycreate("componentA", "statusX") // Creates a new array 
| alter second_part = arraycreate("typeB", "severityY")   // Creates another new array 
| alter combined_info = arrayconcat(first_part, second_part) // Concatenates the two new arrays 
| fields event_id, first_part, second_part, combined_info 
| limit 2 
```

**Explanation**: For each record, two literal arrays, `first_part` and `second_part`, are created. The function then combines the elements of `first_part` followed by `second_part` into the `combined_info` array.

**Output**:

| EVENT\_ID | FIRST\_PART                | SECOND\_PART            | COMBINED\_INFO                                   |
| --------- | -------------------------- | ----------------------- | ------------------------------------------------ |
| 101       | \["componentA", "statusX"] | \["typeB", "severityY"] | \["componentA", "statusX", "typeB", "severityY"] |
| 102       | \["componentA", "statusX"] | \["typeB", "severityY"] | \["componentA", "statusX", "typeB", "severityY"] |

### Example 2: Concatenating an existing array field with a newly created array

**Goal**: Combine the `string_tags` array field from the dataset with a new array created using `arraycreate()`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter new_event_tags = arraycreate("audit", "compliance") // Creates a new array of tags 
| alter extended_string_tags = arrayconcat(string_tags, new_event_tags) // Concatenates existing string_tags with the new tags 
| fields event_id, string_tags, new_event_tags, extended_string_tags 
| limit 3 
```

**Explanation**: For each event, `new_event_tags` is created. The existing `string_tags` are then concatenated with the elements from `new_event_tags` to form `extended_string_tags`. For example, event\_id 101's tags are expanded to include "audit" and "compliance".

**Output**:

| EVENT\_ID | STRING\_TAGS                | NEW\_EVENT\_TAGS         | EXTENDED\_STRING\_TAGS                             |
| --------- | --------------------------- | ------------------------ | -------------------------------------------------- |
| 101       | \["security", "login"]      | \["audit", "compliance"] | \["security", "login", "audit", "compliance"]      |
| 102       | \["filesystem", "critical"] | \["audit", "compliance"] | \["filesystem", "critical", "audit", "compliance"] |
| 103       | \["network", "cloud"]       | \["audit", "compliance"] | \["network", "cloud", "audit", "compliance"]       |

### Example 3: Concatenating multiple derived arrays

**Goal**: Combine portions of the `numeric_codes` array using `arrayrange()` and a newly created array, demonstrating concatenation with more than two inputs.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_two_codes = arrayrange(numeric_codes, 0, 2) // Extracts elements at index 0 and 1 
| alter next_two_codes = arrayrange(numeric_codes, 2, 4)   // Extracts elements at index 2 and 3 
| alter additional_codes = arraycreate(999, 1000)        // Creates an array with two new numbers 
| alter all_combined_codes = arrayconcat(first_two_codes, next_two_codes, additional_codes) // Concatenates three arrays 
| fields event_id, numeric_codes, first_two_codes, next_two_codes, additional_codes, all_combined_codes 
| limit 3 
```

**Explanation**: `arrayrange()` extracts specific slices (sub-arrays) from the `numeric_codes` array. `arraycreate()` is used to define an additional array. The function then takes these two derived arrays and the `additional_codes` array, joining all their elements into `all_combined_codes`.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | FIRST\_TWO\_CODES | NEXT\_TWO\_CODES | ADDITIONAL\_CODES | ALL\_COMBINED\_CODES           |
| --------- | -------------------------- | ----------------- | ---------------- | ----------------- | ------------------------------ |
| 101       | \[13, -47, 29, 82, -15]    | \[13, -47]        | \[29, 82]        | \[999, 1000]      | \[13, -47, 29, 82, 999, 1000]  |
| 102       | \[-21, 56, 13, -88, 42]    | \[-21, 56]        | \[13, -88]       | \[999, 1000]      | \[-21, 56, 13, -88, 999, 1000] |
| 103       | \[90, -33, 7, 51, -62, 18] | \[90, -33]        | \[7, 51]         | \[999, 1000]      | \[90, -33, 7, 51, 999, 1000]   |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`arraycreate`](arraycreate), [`arraydistinct`](arraydistinct), [`arrayrange`](arrayrange)
