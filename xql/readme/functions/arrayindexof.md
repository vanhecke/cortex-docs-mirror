# arrayindexof

Use the `arrayindexof()` function to return the index of the first occurrence of a specified element in an array that satisfies a condition, or 0 if a general boolean condition matches.

## Syntax

```sql
arrayindexof (<array>, <condition>)
arrayindexof (<array>, "@element"<operator>"<array element>")
```

## Parameters

| Name            | Type                            | Required | Description                                                                                |
| --------------- | ------------------------------- | -------- | ------------------------------------------------------------------------------------------ |
| `array`         | array                           | Yes      | The array field to evaluate.                                                               |
| `condition`     | boolean                         | No       | A boolean expression that evaluates to true or false for the array.                        |
| `@element`      | keyword                         | No       | A special keyword representing each individual element within the array during evaluation. |
| `operator`      | operator                        | No       | Any supported XQL comparison operator, such as `=`, `!=`, `>`, `<`, `>=`, `<=`.            |
| `array_element` | string, integer, float, boolean | No       | The value or condition against which each array element is compared.                       |

## Returns

The `arrayindexof()` function returns an integer (0 or a 0-based index) or NULL.

## Usage notes

* If the condition is a general boolean expression not using `@element`, the function returns `0` if the array is not empty and the condition is true.
* If the condition uses `@element` to check individual array elements, the function returns the **0-based index** of the **first** array element that satisfies the condition.
* If the input array is empty, `arrayindexof()` returns `NULL`.
* If the condition (general or `@element`-based) is not met by any element, the function returns `NULL`.

## Examples

### Example 1: General condition - checking array length

**Goal**: Check if the `string_tags` array contains more than one element using a general condition.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter has_multiple_tags = arrayindexof(string_tags, array_length(string_tags) > 1) 
| fields event_id, string_tags, has_multiple_tags 
| limit 4 
```

**Explanation**: The query uses the `arrayindexof(<array>, <condition>)` variant. For `event_id` 101, 102, and 103, the length is 2, so the condition matches and returns `0`. For `event_id` 104, the length is 1, so the condition fails and returns `NULL`.

**Output**:

| EVENT\_ID | STRING\_TAGS                | HAS\_MULTIPLE\_TAGS |
| --------- | --------------------------- | ------------------- |
| 101       | \["security", "login"]      | 0                   |
| 102       | \["filesystem", "critical"] | 0                   |
| 103       | \["network", "cloud"]       | 0                   |
| 104       | \["monitoring"]             | NULL                |

### Example 2: Element-specific condition - checking for a specific string value

**Goal**: Find the index of the first occurrence of the tag "login" in the `string_tags` array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_index_of_login_tag = arrayindexof(string_tags, "@element" = "login") 
| fields event_id, string_tags, first_index_of_login_tag 
| limit 5 
```

**Explanation**: The query uses the `@element` keyword to check each item. For `event_id` 101, "login" is found at index 1, so `1` is returned. For other events where "login" is missing, `NULL` is returned.

**Output**:

| EVENT\_ID | STRING\_TAGS                | FIRST\_INDEX\_OF\_LOGIN\_TAG |
| --------- | --------------------------- | ---------------------------- |
| 101       | \["security", "login"]      | 1                            |
| 102       | \["filesystem", "critical"] | NULL                         |
| 103       | \["network", "cloud"]       | NULL                         |
| 104       | \["monitoring"]             | NULL                         |
| 105       | \["data\_ops"]              | NULL                         |

### Example 3: Element-specific condition - checking for a numeric value greater than a threshold

**Goal**: Find the index of the first numeric code in the `numeric_codes` array that is greater than 50.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_index_of_large_code = arrayindexof(numeric_codes, "@element" > 50) 
| fields event_id, numeric_codes, first_index_of_large_code 
| limit 6 
```

**Explanation**: This query searches the entire array and returns the index of the **first** match. For `event_id` 101, 82 is the first value > 50 (at index 3). For `event_id` 102, 56 is the first match (at index 1).

**Output**:

| EVENT\_ID | NUMERIC\_CODES              | FIRST\_INDEX\_OF\_LARGE\_CODE |
| --------- | --------------------------- | ----------------------------- |
| 101       | \[13, -47, 29, 82, -15]     | 3                             |
| 102       | \[-21, 56, 13, -88, 42]     | 1                             |
| 103       | \[90, -33, 7, 51, -62, 18]  | 0                             |
| 104       | \[]                         | NULL                          |
| 105       | \[77, -9, 35, -47, 61]      | 0                             |
| 106       | \[-12, 24, 68, -59, 37, 80] | 2                             |

### Example 4: Element-specific condition - checking for a value not equal to a specific string

**Goal**: Find the index of the first element in `string_tags` that is not "security".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter first_index_of_non_security = arrayindexof(string_tags, "@element" != "security") 
| fields event_id, string_tags, first_index_of_non_security 
| limit 5 
```

**Explanation**: For `event_id` 101, "security" is at index 0, but "login" is at index 1 and matches the condition `!= "security"`, so `1` is returned. For `event_id` 102, "filesystem" at index 0 matches, so `0` is returned.

**Output**:

| EVENT\_ID | STRING\_TAGS                | FIRST\_INDEX\_OF\_NON\_SECURITY |
| --------- | --------------------------- | ------------------------------- |
| 101       | \["security", "login"]      | 1                               |
| 102       | \["filesystem", "critical"] | 0                               |
| 103       | \["network", "cloud"]       | 0                               |
| 104       | \["monitoring"]             | 0                               |
| 105       | \["data\_ops"]              | 0                               |

### Example 5: Handling an empty array explicitly

**Goal**: Demonstrate that `arrayindexof()` returns `NULL` when applied to an empty array.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 104 // Focus on the event with an empty array 
| alter index_in_empty_array = arrayindexof(numeric_codes, "@element" = 0) 
| fields event_id, numeric_codes, index_in_empty_array 
| limit 1 
```

**Explanation**: For `event_id` 104, the `numeric_codes` array is empty. As per the function's definition, if the array is empty, `NULL` is returned.

**Output**:

| EVENT\_ID | NUMERIC\_CODES | INDEX\_IN\_EMPTY\_ARRAY |
| --------- | -------------- | ----------------------- |
| 104       | \[]            | NULL                    |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`filter`](../stages/filter), [`limit`](../stages/limit)
* **Functions**: [`array_length`](array_length)
