# array\_any

Use the `array_any()` function to determine if at least one element within a specified array satisfies a defined boolean condition. If at least one element meets the condition, the function returns `true`.

## Syntax

```sql
array_any (<array>, "@element"<operator>"<array_element>")
```

## Parameters

| Name        | Type   | Required | Description                                                                                                                                                                                                 |
| ----------- | ------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `array`     | array  | Yes      | The array field to be evaluated.                                                                                                                                                                            |
| `condition` | string | Yes      | A comparison expression enclosed in quotes. The condition must use the special keyword `@element` to represent the individual item being checked, followed by an operator and the value to compare against. |

## Returns

The `array_any()` function returns a boolean value (`true` or `false`).

## Usage notes

* The function iterates through the array and applies the condition to each element individually.
* The function implements a logical "OR" operation across the elements. If **any** single element satisfies the condition, the function returns `true`.
* If the input array is empty, the function returns `false`.
* Supported operators within the condition include standard comparison operators such as `=`, `!=`, `>`, `<`, `>=`, and `<=`.
* This function is typically used within the `alter` or `filter` stages to categorize data or narrow down results based on array contents.

## Examples

### Example 1: Check for specific string value

**Goal**: Check if the `string_tags` array contains the specific value "security".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter any_tag_is_security = array_any(string_tags, "@element" = "security") 
| fields event_id, string_tags, any_tag_is_security 
| limit 6 
```

**Explanation**: The query evaluates the `string_tags` array for each event. If the string "security" is present as any element in the array, `any_tag_is_security` is set to `true`.

**Output**:

| EVENT\_ID | STRING\_TAGS                | ANY\_TAG\_IS\_SECURITY |
| --------- | --------------------------- | ---------------------- |
| 101       | \["security", "login"]      | true                   |
| 102       | \["filesystem", "critical"] | false                  |
| 103       | \["network", "cloud"]       | false                  |
| 104       | \[]                         | false                  |
| 105       | \["data\_ops"]              | false                  |
| 106       | \["security", "attack"]     | true                   |

### Example 2: Check numeric threshold

**Goal**: Determine if any number within the `numeric_codes` array is greater than 50.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter any_code_gt_50 = array_any(numeric_codes, "@element" > 50) 
| fields event_id, numeric_codes, any_code_gt_50 
| limit 5 
```

**Explanation**: The query checks the `numeric_codes` array. If at least one number in the array is greater than 50, the result is `true`. Empty arrays return `false`.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | ANY\_CODE\_GT\_50 |
| --------- | -------------------------- | ----------------- |
| 101       | \[13, -47, 29, 82, -15]    | true              |
| 102       | \[-21, 56, 13, -88, 42]    | true              |
| 103       | \[90, -33, 7, 51, -62, 18] | true              |
| 104       | \[]                        | false             |
| 105       | \[77, -9, 35, -47, 61]     | true              |

### Example 3: Check inequality

**Goal**: Determine if at least one tag in the `string_tags` array is **not** equal to "security".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter any_tag_is_not_security = array_any(string_tags, "@element" != "security") 
| fields event_id, string_tags, any_tag_is_not_security 
| limit 6 
```

**Explanation**: The query returns `true` if it finds any element in the array that is not "security". For example, in event 101, even though "security" is present, the presence of "login" (which is != "security") makes the result `true`.

**Output**:

| EVENT\_ID | STRING\_TAGS                | ANY\_TAG\_IS\_NOT\_SECURITY |
| --------- | --------------------------- | --------------------------- |
| 101       | \["security", "login"]      | true                        |
| 102       | \["filesystem", "critical"] | true                        |
| 103       | \["network", "cloud"]       | true                        |
| 104       | \[]                         | false                       |
| 105       | \["data\_ops"]              | true                        |
| 106       | \["security", "attack"]     | true                        |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`array_all`](array_all), [`arrayfilter`](arrayfilter)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
