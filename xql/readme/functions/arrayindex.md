# arrayindex

Use the `arrayindex()` function to retrieve a single element from a specified array by its numerical position, or index.

## Syntax

```sql
arrayindex (<array>, <index>)
```

## Parameters

| Name    | Type    | Required | Description                                                                                                                                              |
| ------- | ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `array` | array   | Yes      | The array from which you want to extract an element.                                                                                                     |
| `index` | integer | Yes      | An integer representing the zero-based position of the element you want to retrieve (for example, 0 for the first element, 1 for the second, and so on). |

## Returns

The `arrayindex()` function returns a single value, which is the element located at the specified index within the array.

## Usage notes

* Array elements are accessed using a zero-based index, meaning the first element is at index `0`, the second at index `1`, etc.
* If the specified index is beyond the array's boundaries or if the array itself is empty, `arrayindex()` will return `NULL` for the field and not an empty array.
* This function supports negative indices (for example, `-1` for the last element, `-2` for the second to last element).

## Examples

### Example 1: Extracting the first element (Index 0) from a string array

**Goal**: Retrieve the first string tag from the `string_tags` array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_tag = arrayindex(string_tags, 0) // Extracts the first element 
| fields event_id, string_tags, first_tag 
| limit 3 
```

**Explanation**: For each `event_id`, the function extracts the first string element (index 0) from the `string_tags` array.

**Output**:

| event\_id | string\_tags                | first\_tag   |
| --------- | --------------------------- | ------------ |
| 101       | \["security", "login"]      | "security"   |
| 102       | \["filesystem", "critical"] | "filesystem" |
| 103       | \["network", "cloud"]       | "network"    |

### Example 2: Extracting a middle element (Index 2) from a numeric array

**Goal**: Retrieve the third numeric code (at index 2) from the `numeric_codes` array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter third_numeric_code = arrayindex(numeric_codes, 2) // Extracts the element at index 2 
| fields event_id, numeric_codes, third_numeric_code 
| limit 3 
```

**Explanation**: For each `event_id`, the function extracts the element at index 2 (the third element) from the `numeric_codes` array.

**Output**:

| event\_id | numeric\_codes             | third\_numeric\_code |
| --------- | -------------------------- | -------------------- |
| 101       | \[13, -47, 29, 82, -15]    | 29                   |
| 102       | \[-21, 56, 13, -88, 42]    | 13                   |
| 103       | \[90, -33, 7, 51, -62, 18] | 7                    |

### Example 3: Handling an empty array

**Goal**: Demonstrate the behavior when attempting to extract an element from an empty array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 104 // Focus on the event with an empty array 
| alter first_numeric_code_empty = arrayindex(numeric_codes, 0) // Attempt to extract from empty array 
| fields event_id, numeric_codes, first_numeric_code_empty 
| limit 1 
```

**Explanation**: For `event_id` 104, the `numeric_codes` array is empty. As expected, the function returns `NULL` when no element exists at the specified index due to an empty array.

**Output**:

| event\_id | numeric\_codes | first\_numeric\_code\_empty |
| --------- | -------------- | --------------------------- |
| 104       | \[]            | NULL                        |

### Example 4: Handling an out-of-bounds index

**Goal**: Demonstrate the behavior when the specified index is beyond the actual size of the array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter out_of_bounds_code = arrayindex(numeric_codes, 100) // Index 100 is far beyond array size 
| fields event_id, numeric_codes, out_of_bounds_code 
| limit 3 
```

**Explanation**: For all `event_ids`, `numeric_codes` does not have an element at index 100. The function correctly returns `NULL` when the index is out of bounds.

**Output**:

| event\_id | numeric\_codes             | out\_of\_bounds\_code |
| --------- | -------------------------- | --------------------- |
| 101       | \[13, -47, 29, 82, -15]    | NULL                  |
| 102       | \[-21, 56, 13, -88, 42]    | NULL                  |
| 103       | \[90, -33, 7, 51, -62, 18] | NULL                  |

### Example 5: Retrieving the last element (-1 Index)

**Goal**: Extract the last element from an array using the negative index `-1`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter last_numeric_code = arrayindex(numeric_codes, -1) // Extracts the last element using negative index 
| fields event_id, numeric_codes, last_numeric_code 
| limit 3 
```

**Explanation**: Using index `-1` retrieves the final element of the `numeric_codes` array for each record.

**Output**:

| event\_id | numeric\_codes             | last\_numeric\_code |
| --------- | -------------------------- | ------------------- |
| 101       | \[13, -47, 29, 82, -15]    | -15                 |
| 102       | \[-21, 56, 13, -88, 42]    | 42                  |
| 103       | \[90, -33, 7, 51, -62, 18] | 18                  |

### Example 6: Retrieving the second to last element (-2 Index)

**Goal**: Retrieve the second to last element from an array using the negative index `-2`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter second_to_last_numeric_code = arrayindex(numeric_codes, -2) // Extracts the second to last element 
| fields event_id, numeric_codes, second_to_last_numeric_code 
| limit 3 
```

**Explanation**: Using index `-2` retrieves the element immediately preceding the last element in the `numeric_codes` array.

**Output**:

| event\_id | numeric\_codes             | second\_to\_last\_numeric\_code |
| --------- | -------------------------- | ------------------------------- |
| 101       | \[13, -47, 29, 82, -15]    | 82                              |
| 102       | \[-21, 56, 13, -88, 42]    | -88                             |
| 103       | \[90, -33, 7, 51, -62, 18] | -62                             |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`arraycreate`](arraycreate), [`array_length`](array_length)
