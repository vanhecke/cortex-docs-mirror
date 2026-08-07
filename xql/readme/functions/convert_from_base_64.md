# convert\_from\_base\_64

Use the `convert_from_base_64()` function to decode a base64-encoded input string and return it in its original, decoded string format.

## Syntax

```sql
convert_from_base_64 ("<base64-encoded input>")
```

## Parameters

| Name             | Type   | Required | Description                          |
| ---------------- | ------ | -------- | ------------------------------------ |
| `encoded_string` | string | Yes      | The base64-encoded string to decode. |

## Returns

The `convert_from_base_64()` function returns the decoded value as a string.

## Usage notes

* The function requires a single string input that is base64-encoded.
* The function consistently returns the decoded value as a string.
* The function is typically employed within the `alter` stage to create new fields or modify existing ones by decoding string data.
* The function can also be used within a `filter` stage if the decoding result is needed for a conditional check.

## Examples

### Example 1: Decoding a basic literal base64 string

**Goal**: Decode a common base64 string that represents "Hello world".

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter decoded_string = convert_from_base_64("SGVsbG8gd29ybGQ=") 
| fields event_id, decoded_string 
| limit 3 
```

**Explanation**: This query adds a new field, `decoded_string`, which contains the plain text "Hello world" after decoding the provided base64 literal.

**Output**:

| EVENT\_ID | DECODED\_STRING |
| --------- | --------------- |
| 101       | "Hello world"   |
| 102       | "Hello world"   |
| 103       | "Hello world"   |

### Example 2: Decoding a literal base64 string representing JSON

**Goal**: Decode a base64 string that, when decoded, forms a JSON object. This shows the ability to handle more complex string content.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter decoded_json_string = convert_from_base_64("eyJsZXZlbCI6ICJpbmZvIiwgIm1lc3NhZ2UiOiAiU3lzdGVtIHN0YXJ0ZWQifQ==") 
| fields event_id, decoded_json_string 
| limit 3 
```

**Explanation**: The query decodes the base64 string, resulting in a JSON-formatted string as the value for `decoded_json_string`.

**Output**:

| EVENT\_ID | DECODED\_JSON\_STRING                            |
| --------- | ------------------------------------------------ |
| 101       | "{"level": "info", "message": "System started"}" |
| 102       | "{"level": "info", "message": "System started"}" |
| 103       | "{"level": "info", "message": "System started"}" |

### Example 3: Handling an invalid base64 input

**Goal**: Illustrate the function's behavior when provided with a string that is not a valid base64 encoding.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter invalid_decode_attempt = convert_from_base_64("NotABase64String!") 
| fields event_id, invalid_decode_attempt 
| limit 3 
```

**Explanation**: When the input string is not a valid base64 format, the `convert_from_base_64()` function still attempts to return the decoded string.

**Output**:

| EVENT\_ID | INVALID\_DECODE\_ATTEMPT |
| --------- | ------------------------ |
| 101       | "6@\u0005\u001e넭)"       |
| 102       | "6@\u0005\u001e넭)"       |
| 103       | "6@\u0005\u001e넭)"       |

### Example 4: Decoding an empty base64 string

**Goal**: Show the result of decoding an empty base64 string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter decoded_empty_string = convert_from_base_64("") 
| fields event_id, decoded_empty_string 
| limit 3 
```

**Explanation**: Decoding an empty base64 string results in an empty string.

**Output**:

| EVENT\_ID | DECODED\_EMPTY\_STRING |
| --------- | ---------------------- |
| 101       | ""                     |
| 102       | ""                     |
| 103       | ""                     |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/comp), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`convert_to_base_64`](convert_to_base_64)
