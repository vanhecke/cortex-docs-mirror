# extract\_url\_pub\_suffix

Use the `extract_url_pub_suffix()` function to return the public suffix of a given URL string (for example, "com", "org", "net").

## Syntax

```sql
extract_url_pub_suffix ("<URL>")
```

## Parameters

| Name    | Type   | Required | Description                                                                                              |
| ------- | ------ | -------- | -------------------------------------------------------------------------------------------------------- |
| `<URL>` | string | Yes      | The input string literal or field containing the URL from which the public suffix needs to be extracted. |

## Returns

The `extract_url_pub_suffix()` function returns a string representing the public suffix of the URL.

## Usage notes

* The function requires a string value representing a URL as input.
* The function always returns the public suffix value in lowercase characters, regardless of the input URL's original casing.
* This function is typically used within the `alter` stage to create new fields or modify existing ones based on extracted URL data, or within the `filter` stage for conditional logic.

## Examples

### Example 1: Basic public suffix extraction from a standard URL

**Goal**: Extract the public suffix from a common HTTPS URL.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_pub_suffix = extract_url_pub_suffix("https://www.paloaltonetworks.com") 
| fields event_id, extracted_pub_suffix 
| limit 1 
```

**Explanation**: The query extracts "com" as the public suffix from the URL "https://www.paloaltonetworks.com".

**Output**:

| EVENT\_ID | EXTRACTED\_PUB\_SUFFIX |
| --------- | ---------------------- |
| 101       | "com"                  |

### Example 2: Public suffix extraction from a URL with multiple suffixes/paths

**Goal**: correctly identify only the public suffix from a URL that includes subdomains and extended paths.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_pub_suffix_complex = extract_url_pub_suffix("https://www.test.paloaltonetworks.com/suffix/another_suffix") 
| fields event_id, extracted_pub_suffix_complex 
| limit 1 
```

**Explanation**: The function correctly isolates "com" as the public suffix, ignoring subdomains and path components.

**Output**:

| EVENT\_ID | EXTRACTED\_PUB\_SUFFIX\_COMPLEX |
| --------- | ------------------------------- |
| 101       | "com"                           |

### Example 3: Public suffix extraction with mixed-case input

**Goal**: Demonstrate that the function returns the public suffix in lowercase characters, even if the input URL contains uppercase letters.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_pub_suffix_lowercase = extract_url_pub_suffix("www.Example.Co.UK") 
| fields event_id, extracted_pub_suffix_lowercase 
| limit 1 
```

**Explanation**: Despite "www.Example.Co.UK" having mixed casing, the function returns "uk" in all lowercase, demonstrating its built-in lowercasing behavior.

**Output**:

| EVENT\_ID | EXTRACTED\_PUB\_SUFFIX\_LOWERCASE |
| --------- | --------------------------------- |
| 101       | "uk"                              |

### Example 4: Handling NULL input

**Goal**: Demonstrate the function's behavior when provided with a NULL input.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter null_url_input = NULL 
| alter extracted_pub_suffix_from_null = extract_url_pub_suffix(null_url_input) 
| fields event_id, null_url_input, extracted_pub_suffix_from_null 
| limit 1 
```

**Explanation**: Consistent with standard XQL function behavior, if the input to `extract_url_pub_suffix()` is NULL, the function returns NULL.

**Output**:

| EVENT\_ID | NULL\_URL\_INPUT | EXTRACTED\_PUB\_SUFFIX\_FROM\_NULL |
| --------- | ---------------- | ---------------------------------- |
| 101       | NULL             | NULL                               |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`filter`](../stages/filter)
* **Functions**: [`extract_url_host`](extract_url_host), [`extract_url_registered_domain`](extract_url_registered_domain)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
