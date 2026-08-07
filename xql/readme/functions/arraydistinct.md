# arraydistinct

Use the `arraydistinct()` function to return a new array containing only the unique values found in the original input array.

## Syntax

```sql
arraydistinc (<array>)
```

## Parameters

| Name    | Type  | Required | Description                                            |
| ------- | ----- | -------- | ------------------------------------------------------ |
| `array` | array | Yes      | The array field from which to extract unique elements. |

## Returns

The `arraydistinct()` function returns a new array, where all elements are unique.

## Usage notes

* Only one instance of each value is retained in the resulting array.
* The function operates on elements as they are typed. For example, if "100" (string) and 100 (number) were distinct elements in the input array, they would be considered distinct in the output.
* If the input array is empty, `arraydistinct()` will return an empty array.

## Examples

### Example 1: Removing duplicate string literals from a newly created array

**Goal**: Create an array with intentional string duplicates and then process it to retain only unique string values.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter raw_array_with_duplicates = arraycreate("alert", "security", "alert", "investigation_needed", "security") 
| alter distinct_tags = arraydistinct(raw_array_with_duplicates) 
| fields event_id, raw_array_with_duplicates, distinct_tags 
| limit 3 
```

**Explanation**: A new field `raw_array_with_duplicates` is created for each record using `arraycreate()`, containing repeated string values "alert" and "security". `arraydistinct()` is then applied to produce `distinct_tags`, which contains only the unique string values.

**Output**:

| EVENT\_ID | RAW\_ARRAY\_WITH\_DUPLICATES                                         | DISTINCT\_TAGS                                  |
| --------- | -------------------------------------------------------------------- | ----------------------------------------------- |
| 101       | \["alert", "security", "alert", "investigation\_needed", "security"] | \["alert", "security", "investigation\_needed"] |
| 102       | \["alert", "security", "alert", "investigation\_needed", "security"] | \["alert", "security", "investigation\_needed"] |
| 103       | \["alert", "security", "alert", "investigation\_needed", "security"] | \["alert", "security", "investigation\_needed"] |

### Example 2: Removing duplicate numeric literals from a newly created array

**Goal**: Process an array composed of numeric literals, including duplicates, and yield an array with only unique numeric values.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter raw_numbers_with_duplicates = arraycreate(100, 50, 100, 50, 25, 100) 
| alter distinct_numbers = arraydistinct(raw_numbers_with_duplicates) 
| fields event_id, raw_numbers_with_duplicates, distinct_numbers 
| limit 3 
```

**Explanation**: `raw_numbers_with_duplicates` is created as an array of integers with repeated values. `arraydistinct()` effectively identifies and removes these numerical duplicates, resulting in `distinct_numbers` containing only the unique integer values.

**Output**:

| EVENT\_ID | RAW\_NUMBERS\_WITH\_DUPLICATES | DISTINCT\_NUMBERS |
| --------- | ------------------------------ | ----------------- |
| 101       | \[100, 50, 100, 50, 25, 100]   | \[100, 50, 25]    |
| 102       | \[100, 50, 100, 50, 25, 100]   | \[100, 50, 25]    |
| 103       | \[100, 50, 100, 50, 25, 100]   | \[100, 50, 25]    |

### Example 3: Applying `arraydistinct()` to an existing array field

**Goal**: Demonstrate how `arraydistinct()` handles an existing array field that does not contain duplicates within its individual elements.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter original_tags = string_tags 
| alter processed_tags = arraydistinct(original_tags) 
| fields event_id, original_tags, processed_tags 
| limit 3 
```

**Explanation**: The `original_tags` field holds the existing `string_tags` array. `arraydistinct()` processes this array to produce `processed_tags`. In cases where the original array contains no duplicates, the output array will be identical to the input.

**Output**:

| EVENT\_ID | ORIGINAL\_TAGS              | PROCESSED\_TAGS             |
| --------- | --------------------------- | --------------------------- |
| 101       | \["security", "login"]      | \["security", "login"]      |
| 102       | \["filesystem", "critical"] | \["filesystem", "critical"] |
| 103       | \["network", "cloud"]       | \["network", "cloud"]       |

### Example 4: `arraydistinct()` on an array constructed from mixed field values with duplicates

**Goal**: Build an array by combining elements from different fields, introducing an explicit duplicate, and then use `arraydistinct()` to resolve it.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_tag = arrayindex(string_tags, 0) 
| alter combined_values_raw = arraycreate(first_tag, first_tag, to_string(event_id)) 
| alter unique_combined_values = arraydistinct(combined_values_raw) 
| fields event_id, combined_values_raw, unique_combined_values 
| limit 3 
```

**Explanation**: `combined_values_raw` is constructed using string elements (`first_tag` repeated, and `event_id` converted to a string), creating a duplicate. `arraydistinct()` processes this array, removing the repeated `first_tag` to yield `unique_combined_values`.

**Output**:

| EVENT\_ID | COMBINED\_VALUES\_RAW                | UNIQUE\_COMBINED\_VALUES |
| --------- | ------------------------------------ | ------------------------ |
| 101       | \["security", "security", "101"]     | \["security", "101"]     |
| 102       | \["filesystem", "filesystem", "102"] | \["filesystem", "102"]   |
| 103       | \["network", "network", "103"]       | \["network", "103"]      |

### Example 5: `arraydistinct()` on a concatenated array with duplicates

**Goal**: Use `arraydistinct()` on an array formed by concatenating an existing array with itself, which inherently introduces duplicates.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter duplicate_numeric_codes = numeric_codes 
| alter duplicated_numeric_array = arrayconcat(numeric_codes, duplicate_numeric_codes) 
| alter distinct_concatenated_numeric = arraydistinct(duplicated_numeric_array) 
| fields event_id, duplicate_numeric_codes, duplicated_numeric_array, distinct_concatenated_numeric 
| limit 3 
```

**Explanation**: `arrayconcat()` is used to join the `numeric_codes` array with itself, creating `duplicated_numeric_array`. `arraydistinct()` is then applied, effectively reducing it back to the original set of unique elements in `distinct_concatenated_numeric`.

**Output**:

| EVENT\_ID | DUPLICATE\_NUMERIC\_CODES  | DUPLICATED\_NUMERIC\_ARRAY                          | DISTINCT\_CONCATENATED\_NUMERIC |
| --------- | -------------------------- | --------------------------------------------------- | ------------------------------- |
| 101       | \[13, -47, 29, 82, -15]    | \[13, -47, 29, 82, -15, 13, -47, 29, 82, -15]       | \[13, -47, 29, 82, -15]         |
| 102       | \[-21, 56, 13, -88, 42]    | \[-21, 56, 13, -88, 42, -21, 56, 13, -88, 42]       | \[-21, 56, 13, -88, 42]         |
| 103       | \[90, -33, 7, 51, -62, 18] | \[90, -33, 7, 51, -62, 18, 90, -33, 7, 51, -62, 18] | \[90, -33, 7, 51, -62, 18]      |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`arraycreate`](arraycreate), [`arrayindex`](arrayindex), [`arrayconcat`](arrayconcat), [`to_string`](to_string)
