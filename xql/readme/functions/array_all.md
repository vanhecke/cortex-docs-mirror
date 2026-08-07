# array\_all

Use the `array_all()` function to determine if all elements within a specified array satisfy a defined boolean condition.

## Syntax

```sql
array_all (<array>, "@element"<operator>"<array_element>")
```

## Parameters

| Name            | Type                            | Required | Description                                                                                |
| --------------- | ------------------------------- | -------- | ------------------------------------------------------------------------------------------ |
| `array`         | array                           | Yes      | The array field to evaluate.                                                               |
| `@element`      | keyword                         | Yes      | A special keyword representing each individual element within the array during evaluation. |
| `operator`      | string                          | Yes      | Any supported XQL comparison operator (for example, `=`, `!=`, `>`, `<`, `>=`, `<=`).      |
| `array_element` | string, integer, float, boolean | Yes      | The value or condition against which each array element is compared.                       |

## Returns

The `array_all()` function returns a boolean value (`true` or `false`). The function returns `true` only if every single element in the array meets the condition; otherwise, the function returns `false`.

## Usage notes

* The function implements a strict "AND" operation across all elements. If even one element fails the condition, the entire function returns `false`.
* The `array_all()` function will return `false` if run against an empty array.
* The function is typically used within the `alter` or `filter` stages for data transformation or narrowing down results.

## Examples

### Example 1: Checking if all string tags are a specific value

**Goal**: Verify if every tag in the `string_tags` array is exactly "security".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter all_tags_are_security = array_all(string_tags, "@element" = "security") 
| fields event_id, string_tags, all_tags_are_security 
| limit 5
```

**Explanation**: For `event_id` 101, the array `["security", "login"]` returns `false` because "login" is not "security". For `event_id` 104, `[]` (an empty array) returns `false`.

**Output**:

| EVENT\_ID | STRING\_TAGS                | ALL\_TAGS\_ARE\_SECURITY |
| --------- | --------------------------- | ------------------------ |
| 101       | \["security", "login"]      | false                    |
| 102       | \["filesystem", "critical"] | false                    |
| 103       | \["network", "cloud"]       | false                    |
| 104       | \[]                         | false                    |
| 105       | \["data\_ops"]              | false                    |

### Example 2: Checking if all numeric codes are greater than zero

**Goal**: Evaluate if every number in the `numeric_codes` array is greater than zero.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter all_codes_positive = array_all(numeric_codes, "@element" > 0) 
| fields event_id, numeric_codes, all_codes_positive 
| limit 5
```

**Explanation**: For `event_id` 101, the array `[13, -47, 29, 82, -15]` returns `false` because elements like -47 and -15 are not greater than zero. For `event_id` 104, `[]` (an empty array) returns `false`.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | ALL\_CODES\_POSITIVE |
| --------- | -------------------------- | -------------------- |
| 101       | \[13, -47, 29, 82, -15]    | false                |
| 102       | \[-21, 56, 13, -88, 42]    | false                |
| 103       | \[90, -33, 7, 51, -62, 18] | false                |
| 104       | \[]                        | false                |
| 105       | \[77, -9, 35, -47, 61]     | false                |

### Example 3: Checking if all string tags are NOT a specific value

**Goal**: Check if all tags in `string_tags` are not equal to "security" using the `!=` operator.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter none_are_security = array_all(string_tags, "@element" != "security") 
| fields event_id, string_tags, none_are_security 
| limit 5
```

**Explanation**: For `event_id` 101, the array `["security", "login"]` returns `false` because "security" is present in the array, failing the "not equal to security" condition. For `event_id` 102, the array `["filesystem", "critical"]` returns `true` because neither "filesystem" nor "critical" are equal to "security".

**Output**:

| EVENT\_ID | STRING\_TAGS                | NONE\_ARE\_SECURITY |
| --------- | --------------------------- | ------------------- |
| 101       | \["security", "login"]      | false               |
| 102       | \["filesystem", "critical"] | true                |
| 103       | \["network", "cloud"]       | true                |
| 104       | \[]                         | false               |
| 105       | \["data\_ops"]              | true                |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`array_any`](array_any)
