# trim

Use the `trim()` function to remove specified characters or whitespace from the beginning and end of a given string.

## Syntax

```sql
trim (<string>, [trim_characters])
```

## Parameters

| Name              | Type   | Required | Description                                                                                                                                            |
| ----------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `string`          | string | Yes      | The input string field or literal value to be trimmed.                                                                                                 |
| `trim_characters` | string | No       | A string containing the characters you want to remove. If this parameter is omitted, the function will remove whitespace characters (spaces and tabs). |

## Returns

The `trim()` function returns a string with the specified characters or whitespace removed from both the start and end.

## Usage notes

* The function removes characters from both the beginning (left) and end (right) of the string.
* If `trim_characters` is not provided, the function defaults to removing leading and trailing spaces and tabs.
* The function is versatile for cleaning and standardizing string data within queries.

## Examples

### Example 1: Removing leading and trailing whitespace (default behavior)

**Goal**: Remove spaces from both ends of a literal string where no specific characters are defined.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter original_string = "   User login successful   " 
| alter trimmed_string = trim(original_string) 
| fields event_id, original_string, trimmed_string 
| limit 1 
```

**Explanation**: The query detects and removes the leading and trailing spaces from the `original_string`, resulting in a clean string "User login successful".

**Output**:

| EVENT\_ID | ORIGINAL\_STRING          | TRIMMED\_STRING         |
| --------- | ------------------------- | ----------------------- |
| 101       | " User login successful " | "User login successful" |

### Example 2: Removing specific characters from both ends

**Goal**: Remove explicit characters ("w") from both ends of the `dst_domain` string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 103 
| alter domain_without_w = trim(dst_domain, "w")
| fields event_id, dst_domain, domain_without_w 
```

**Explanation**: The function removes all leading and trailing 'w' characters from the `dst_domain` string (for example, "www.google.com" becomes ".google.com").

**Output**:

| EVENT\_ID | DST\_DOMAIN      | DOMAIN\_WITHOUT\_W |
| --------- | ---------------- | ------------------ |
| 103       | "www.google.com" | ".google.com"      |

### Example 3: Removing multiple specific characters

**Goal**: Remove a set of explicit characters ("w", "m", and ".") from both ends of the `dst_domain` string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 110 
| alter domain_without_w_m_period = trim(dst_domain, "wm.")
| fields event_id, dst_domain, domain_without_w_m_period
```

**Explanation**: The function removes all occurrences of 'w', 'm', and '.' characters found at the start or end of the string. For "www.mongodb.com", the leading "www." and the trailing "m" are removed, leaving "ongodb.co".

**Output**:

| EVENT\_ID | DST\_DOMAIN       | DOMAIN\_WITHOUT\_W\_M\_PERIOD |
| --------- | ----------------- | ----------------------------- |
| 110       | "www.mongodb.com" | "ongodb.co"                   |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`ltrim`](ltrim), [`rtrim`](rtrim)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
