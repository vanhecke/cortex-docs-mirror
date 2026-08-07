# arrayfilter

Use the `arrayfilter()` function to create a new array containing only the elements from the original input array that satisfy a specified boolean condition.

## Syntax

```sql
arrayfilter (<array>, <condition>)
```

or

```sql
arrayfilter (<array>, "@element"<operator>"<array_element>")
```

## Parameters

| Name            | Type                            | Required | Description                                                                                                       |
| --------------- | ------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `array`         | array                           | Yes      | The array field to filter.                                                                                        |
| `@element`      | keyword                         | Yes      | A special keyword that refers to each individual element within the array during the evaluation of the condition. |
| `operator`      | operator                        | Yes      | Any supported XQL comparison operator, such as `=`, `!=`, `>`, `<`, `>=`, or `<=`.                                |
| `array_element` | string, integer, float, boolean | Yes      | The value or condition against which each array element is compared.                                              |

## Returns

The `arrayfilter()` function returns a new array containing only the elements that meet the specified condition.

## Usage notes

* The specified condition is applied individually to every element in the input array.
* If the input array is empty, the function will return an empty array.
* This function is commonly used within the `alter` or `filter` stages to perform data transformations or to narrow down query results.

## Examples

### Example 1: Filtering a string array for specific elements

**Goal**: Filter the `string_tags` array to include only tags that match the specific value "security".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter security_tags = arrayfilter(string_tags, "@element" = "security") 
| fields event_id, string_tags, security_tags 
| limit 3 
```

**Explanation**: For `event_id` 101, "security" matches the condition, so it is included in the new array, while "login" is excluded. For events 102 and 103, no elements match, resulting in an empty array.

**Output**:

| EVENT\_ID | STRING\_TAGS                | SECURITY\_TAGS |
| --------- | --------------------------- | -------------- |
| 101       | \["security", "login"]      | \["security"]  |
| 102       | \["filesystem", "critical"] | \[]            |
| 103       | \["network", "cloud"]       | \[]            |

### Example 2: Filtering a numeric array for values greater than a threshold

**Goal**: Filter the `numeric_codes` array to include only numbers greater than 50.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter large_numeric_codes = arrayfilter(numeric_codes, "@element" > 50) 
| fields event_id, numeric_codes, large_numeric_codes 
| limit 3 
```

**Explanation**: The function iterates through the `numeric_codes` array. For `event_id` 101, only 82 is greater than 50. For 102, only 56 is greater. For 103, both 90 and 51 are retained.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | LARGE\_NUMERIC\_CODES |
| --------- | -------------------------- | --------------------- |
| 101       | \[13, -47, 29, 82, -15]    | \[82]                 |
| 102       | \[-21, 56, 13, -88, 42]    | \[56]                 |
| 103       | \[90, -33, 7, 51, -62, 18] | \[90, 51]             |

### Example 3: Filtering a string array for elements not equal to a value

**Goal**: Filter the `string_tags` array to include only tags that are **not** equal to "login".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter non_login_tags = arrayfilter(string_tags, "@element" != "login") 
| fields event_id, string_tags, non_login_tags 
| limit 3 
```

**Explanation**: For `event_id` 101, "security" is not "login", so it is included, while "login" is excluded. For events 102 and 103, all elements satisfy the condition (are not "login"), so the entire arrays are retained.

**Output**:

| EVENT\_ID | STRING\_TAGS                | NON\_LOGIN\_TAGS            |
| --------- | --------------------------- | --------------------------- |
| 101       | \["security", "login"]      | \["security"]               |
| 102       | \["filesystem", "critical"] | \["filesystem", "critical"] |
| 103       | \["network", "cloud"]       | \["network", "cloud"]       |

### Example 4: Filtering an array and checking its length in a filter stage

**Goal**: Create a new array by filtering `string_tags` for elements containing the substring "crit", and then filter the dataset to only show records where this new array is not empty.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter critical_event_tags = arrayfilter(string_tags, "@element" contains "crit") 
| filter array_length(critical_event_tags) > 0 
| fields event_id, string_tags, critical_event_tags 
| limit 3 
```

**Explanation**: First, `critical_event_tags` is created containing only tags that include "crit". For `event_id` 102, this results in `["critical"]`. The `filter` stage then uses `array_length()` to retain only records where the filtered array has elements.

**Output**:

| EVENT\_ID | STRING\_TAGS                | CRITICAL\_EVENT\_TAGS |
| --------- | --------------------------- | --------------------- |
| 102       | \["filesystem", "critical"] | \["critical"]         |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter), [`fields`](../stages/fields)
* **Functions**: [`array_length`](array_length)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
