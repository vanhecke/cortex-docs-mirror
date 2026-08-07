# arraymap

Use the `arraymap()` function to apply a specified callable function to every element of an input array, returning a new array containing the transformed elements.

## Syntax

```sql
arraymap (<array>, <function()>)
```

## Parameters

| Name         | Type     | Required | Description                                                                                                                                              |
| ------------ | -------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `array`      | array    | Yes      | The array whose elements you want to transform.                                                                                                          |
| `function()` | function | Yes      | The function to apply to each element of the array. Use the special keyword `"@element"` as a placeholder for the current array element being processed. |

## Returns

The `arraymap()` function returns a new array, where each element is the result of applying the specified function to the corresponding element of the original array.

## Usage notes

* The function iterates through each element, applies the defined transformation, and collects the results into a new array.
* When the function applied within `arraymap()` needs to reference the current array element being processed, it uses `"@element"` as a placeholder for that element.
* `arraymap()` is typically used within the `alter` or `filter` stages for data transformations.

## Examples

### Example 1: Applying a simple mathematical transformation to a numeric array

**Goal**: Multiply each element in a numeric array by a specific constant.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter multiplied_codes = arraymap(numeric_codes, multiply("@element", 10))
| fields event_id, numeric_codes, multiplied_codes
| limit 4
```

**Explanation**: For each record, `arraymap()` iterates over the `numeric_codes` array. The `multiply()` function takes each `"@element"` (for example, 13) and multiplies it by 10. The results form the new `multiplied_codes` array. An empty input array (event\_id 104) results in an empty output array.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | MULTIPLIED\_CODES                |
| --------- | -------------------------- | -------------------------------- |
| 101       | \[13, -47, 29, 82, -15]    | \[130, -470, 290, 820, -150]     |
| 102       | \[-21, 56, 13, -88, 42]    | \[-210, 560, 130, -880, 420]     |
| 103       | \[90, -33, 7, 51, -62, 18] | \[900, -330, 70, 510, -620, 180] |
| 104       | \[]                        | \[]                              |

### Example 2: Applying a string transformation (uppercase) to a string array

**Goal**: Convert all string elements within an array to uppercase.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter uppercase_tags = arraymap(string_tags, uppercase("@element"))
| fields event_id, string_tags, uppercase_tags
| limit 4
```

**Explanation**: The `arraymap()` function processes each element in `string_tags` (for example, "security"). The `uppercase()` function converts `"@element"` to its uppercase equivalent. The transformed elements form the `uppercase_tags` array.

**Output**:

| EVENT\_ID | STRING\_TAGS                | UPPERCASE\_TAGS             |
| --------- | --------------------------- | --------------------------- |
| 101       | \["security", "login"]      | \["SECURITY", "LOGIN"]      |
| 102       | \["filesystem", "critical"] | \["FILESYSTEM", "CRITICAL"] |
| 103       | \["network", "cloud"]       | \["NETWORK", "CLOUD"]       |
| 104       | \["monitoring"]             | \["MONITORING"]             |

### Example 3: Applying a conditional transformation (replacing negative values) to a numeric array

**Goal**: Replace any negative numbers in an array with 0, while keeping positive numbers unchanged.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter positive_codes = arraymap(numeric_codes, if("@element" < 0, 0, "@element"))
| fields event_id, numeric_codes, positive_codes
| limit 4
```

**Explanation**: For each number in `numeric_codes`, the `if()` function checks if `"@element"` is less than 0. If true, it is replaced with 0; otherwise, the original `"@element"` value is retained.

**Output**:

| EVENT\_ID | NUMERIC\_CODES             | POSITIVE\_CODES        |
| --------- | -------------------------- | ---------------------- |
| 101       | \[13, -47, 29, 82, -15]    | \[13, 0, 29, 82, 0]    |
| 102       | \[-21, 56, 13, -88, 42]    | \[0, 56, 13, 0, 42]    |
| 103       | \[90, -33, 7, 51, -62, 18] | \[90, 0, 7, 51, 0, 18] |
| 104       | \[]                        | \[]                    |

### Example 4: Extracting scalar values from JSON Objects within an array

**Goal**: Iterate through an array of JSON objects and extract a specific scalar value (for example, action or event) from each object into a new array.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter extracted_actions = arraymap(array_of_json_objects, coalesce(
        json_extract_scalar(to_json_string("@element"), "$.action"),
        json_extract_scalar(to_json_string("@element"), "$.event")
    ))
| fields event_id, array_of_json_objects, extracted_actions
| limit 4
```

**Explanation**: `arraymap()` iterates over each JSON object within `array_of_json_objects`. For each `@element` (a JSON object), `to_json_string()` converts it to a string. `json_extract_scalar()` then attempts to extract the `action` field. If not found, it tries to extract the `event` field. `coalesce()` returns the first non-null result.

**Output**:

| EVENT\_ID | ARRAY\_OF\_JSON\_OBJECTS                                                              | EXTRACTED\_ACTIONS |
| --------- | ------------------------------------------------------------------------------------- | ------------------ |
| 101       | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}]  | \["read", "write"] |
| 102       | \[{"event": "file\_open", "path": "/etc/passwd"}]                                     | \["file\_open"]    |
| 103       | \[{"conn\_type": "outbound", "bytes": 1024}, {"conn\_type": "inbound", "bytes": 512}] | \[]                |
| 104       | \[]                                                                                   | \[]                |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`multiply`](multiply), [`uppercase`](uppercase), [`if`](if), [`coalesce`](coalesce), [`json_extract_scalar`](json_extract_scalar), [`to_json_string`](to_json_string)
