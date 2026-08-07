# arrayrange

Use the `arrayrange()` function to return a new array containing a subset of elements from an original array. The subset is defined by a specified start index (inclusive) and an end index (exclusive).

## Syntax

```sql
arrayrange (<array>, <start>, <end>)
```

## Parameters

| Name    | Type    | Required | Description                                                                                   |
| ------- | ------- | -------- | --------------------------------------------------------------------------------------------- |
| `array` | array   | Yes      | The array from which you want to extract a portion.                                           |
| `start` | integer | Yes      | An integer representing the 0-based index where the new array slice should begin (inclusive). |
| `end`   | integer | Yes      | An integer representing the 0-based index where the new array slice should end (exclusive).   |

## Returns

The `arrayrange()` function returns a new XQL-native array, which is a slice of the original array.

## Usage notes

* Array indices in XQL are 0-based, meaning the first element is at index 0.
* The element at the `<start>` index is included, but the element at the `<end>` index is **not** included in the result.
* If the `<end>` index is greater than the last element's actual index in the array, the function will return elements from the `<start>` index up to the end of the original array.
* If the input array is null or empty, or if the start index is out of bounds or greater than or equal to the end index, `arrayrange()` will typically return an empty or null array.

## Examples

### Example 1: Extracting a standard slice from a numeric array

**Goal**: This example demonstrates extracting a portion from the `numeric_codes` array using typical start and end indices.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_three_codes = arrayrange(numeric_codes, 0, 3) // Extracts elements from index 0 up to (but not including) index 3 
| fields event_id, numeric_codes, first_three_codes 
| limit 3 
```

**Explanation**: The `numeric_codes` field contains arrays of integers. `arrayrange(numeric_codes, 0, 3)` creates a new array for each record, taking elements starting from index 0 and stopping before index 3 (i.e., elements at indices 0, 1, and 2).

**Output**:

| event\_id | numeric\_codes             | first\_three\_codes |
| --------- | -------------------------- | ------------------- |
| 101       | \[13, -47, 29, 82, -15]    | \[13, -47, 29]      |
| 102       | \[-21, 56, 13, -88, 42]    | \[-21, 56, 13]      |
| 103       | \[90, -33, 7, 51, -62, 18] | \[90, -33, 7]       |

### Example 2: Extracting a slice where the end index is beyond the array's length

**Goal**: This example demonstrates the behavior of `arrayrange()` when the specified end index exceeds the actual number of elements in the array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter slice_to_end = arrayrange(numeric_codes, 2, 100) // Starts at index 2, goes to actual end if 100 is out of bounds 
| fields event_id, numeric_codes, slice_to_end 
| limit 3 
```

**Explanation**: `arrayrange(numeric_codes, 2, 100)` attempts to extract elements starting from index 2 up to index 99. Because the `numeric_codes` arrays typically have fewer than 100 elements, the function correctly returns all elements from index 2 to the actual end of each array.

**Output**:

| event\_id | numeric\_codes             | slice\_to\_end    |
| --------- | -------------------------- | ----------------- |
| 101       | \[13, -47, 29, 82, -15]    | \[29, 82, -15]    |
| 102       | \[-21, 56, 13, -88, 42]    | \[13, -88, 42]    |
| 103       | \[90, -33, 7, 51, -62, 18] | \[7, 51, -62, 18] |

### Example 3: Extracting a slice from a string array

**Goal**: This example illustrates `arrayrange()` applied to a string array, demonstrating its versatility across different data types.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter middle_tags = arrayrange(string_tags, 1, 3) // Extracts elements from index 1 up to (but not including) index 3 
| fields event_id, string_tags, middle_tags 
| limit 3 
```

**Explanation**: The `string_tags` field contains arrays of strings. `arrayrange(string_tags, 1, 3)` extracts elements starting from index 1 and stopping before index 3. For the sample data, this often results in just the second element as most `string_tags` arrays have only two elements (indices 0 and 1).

**Output**:

| event\_id | string\_tags                | middle\_tags  |
| --------- | --------------------------- | ------------- |
| 101       | \["security", "login"]      | \["login"]    |
| 102       | \["filesystem", "critical"] | \["critical"] |
| 103       | \["network", "cloud"]       | \["cloud"]    |

### Example 4: Handling an empty array input

**Goal**: This example demonstrates how `arrayrange()` behaves when the input array is empty.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 104 // Event ID 104 has an empty 'array_of_json_objects' 
| alter empty_array_slice = arrayrange(array_of_json_objects, 0, 1) // Attempts to extract from an empty array 
| fields event_id, array_of_json_objects, empty_array_slice 
| limit 1 
```

**Explanation**: `event_id` 104 in `sample_xql_raw` has an empty `array_of_json_objects` field. When `arrayrange()` is applied to an empty array, it returns an empty array, indicating that no elements could be extracted from the specified range.

**Output**:

| event\_id | array\_of\_json\_objects | empty\_array\_slice |
| --------- | ------------------------ | ------------------- |
| 104       | \[]                      | \[]                 |

### Example 5: Using `arrayrange()` with dynamically created arrays

**Goal**: This example shows `arrayrange()` applied to an array that is explicitly constructed within the query using `arraycreate()`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter dynamic_numbers = arraycreate(10, 20, 30, 40, 50, 60, 70) // Creates a new array 
| alter dynamic_slice = arrayrange(dynamic_numbers, 2, 5) // Extracts elements from index 2 up to (but not including) index 5 
| fields event_id, dynamic_numbers, dynamic_slice 
| limit 2 
```

**Explanation**: `dynamic_numbers` is a new array created on the fly with a set of integer values. `arrayrange(dynamic_numbers, 2, 5)` then extracts the elements at indices 2, 3, and 4 from this newly created array, resulting in `[30, 40, 50]`.

**Output**:

| event\_id | dynamic\_numbers              | dynamic\_slice |
| --------- | ----------------------------- | -------------- |
| 101       | \[10, 20, 30, 40, 50, 60, 70] | \[30, 40, 50]  |
| 102       | \[10, 20, 30, 40, 50, 60, 70] | \[30, 40, 50]  |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit), [`filter`](../stages/filter)
* **Functions**: [`arraycreate`](arraycreate)
