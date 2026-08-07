# extract\_url\_host

Use the `extract_url_host()` function to return the host portion of a given URL string.

## Syntax

```sql
extract_url_host (<url_string>)
```

## Parameters

| Name         | Type   | Required | Description                                                                                     |
| ------------ | ------ | -------- | ----------------------------------------------------------------------------------------------- |
| `url_string` | string | Yes      | The input string literal or field containing the URL from which the host needs to be extracted. |

## Returns

The `extract_url_host()` function returns a string representing the host of the URL.

## Usage notes

* The function always returns the host value in lowercase characters, regardless of the input URL's original casing.
* This function is typically used within the `alter` stage to create new fields or modify existing ones based on extracted URL data, or within the `filter` stage for conditional logic.
* If the input `url_string` is NULL, the function returns NULL.

## Examples

### Example 1: Basic host extraction from a standard URL

**Goal**: Extract the host from a common HTTPS URL.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_host = extract_url_host("https://www.paloaltonetworks.com") 
| fields event_id, extracted_host 
| limit 1 
```

**Explanation**: The query extracts the host "www.paloaltonetworks.com" from the provided URL string.

**Output**:

| EVENT\_ID | EXTRACTED\_HOST          |
| --------- | ------------------------ |
| 101       | www.paloaltonetworks.com |

### Example 2: Host extraction from a URL with user, password, and port

**Goal**: Extract the host from a complex URL that includes user credentials and port numbers.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_host_complex = extract_url_host("//user:password@a.b:80/path?query") 
| fields event_id, extracted_host_complex 
| limit 1 
```

**Explanation**: `extract_url_host()` successfully isolates "a.b" as the host, ignoring the user, password, port, path, and query parameters.

**Output**:

| EVENT\_ID | EXTRACTED\_HOST\_COMPLEX |
| --------- | ------------------------ |
| 101       | a.b                      |

### Example 3: Host extraction with mixed-case input

**Goal**: Extract the host from a URL containing uppercase letters, demonstrating the automatic lowercasing behavior.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_host_lowercase = extract_url_host("www.Example.Co.UK") 
| fields event_id, extracted_host_lowercase 
| limit 1 
```

**Explanation**: Despite "www.Example.Co.UK" having mixed casing, the function returns "www.example.co.uk" in all lowercase, demonstrating its built-in lowercasing behavior.

**Output**:

| EVENT\_ID | EXTRACTED\_HOST\_LOWERCASE |
| --------- | -------------------------- |
| 101       | \<www.example.co.uk>       |

### Example 4: Host extraction from a URL with multiple suffixes/paths

**Goal**: Extract the full hostname from a URL that includes subdomains and extended paths.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter extracted_host_path = extract_url_host("https://www.test.paloaltonetworks.com/suffix/another_suffix") 
| fields event_id, extracted_host_path 
| limit 1 
```

**Explanation**: The function correctly identifies the entire host, including subdomains, regardless of the trailing path components.

**Output**:

| EVENT\_ID | EXTRACTED\_HOST\_PATH         |
| --------- | ----------------------------- |
| 101       | www.test.paloaltonetworks.com |

### Example 5: Handling NULL input

**Goal**: Demonstrate the function's behavior when provided with a NULL input.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter null_url_input = NULL 
| alter extracted_host_from_null = extract_url_host(null_url_input) 
| fields event_id, null_url_input, extracted_host_from_null 
| limit 1 
```

**Explanation**: Consistent with standard XQL function behavior, if the input to `extract_url_host()` is NULL, the function returns NULL.

**Output**:

| EVENT\_ID | NULL\_URL\_INPUT | EXTRACTED\_HOST\_FROM\_NULL |
| --------- | ---------------- | --------------------------- |
| 101       | NULL             | NULL                        |

### Example: Host extraction from a URL string

**Goal**: Return a single record from the `sample_xql_raw` dataset showing the extracted host name from a specific URL string ("[https://www.test.paloaltonetworks.com](https://www.test.paloaltonetworks.com)").

**XQL Code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter url_host = extract_url_host("https://www.test.paloaltonetworks.com") 
| fields url_host 
| limit 1
```

**Explanation**:

1. The query starts by accessing the xdr\_data dataset.
2. The alter stage creates a new field named url\_host.
3. The extract\_url\_host() function parses the provided URL string and isolates the host component (www.test.paloaltonetworks.com).
4. The fields stage restricts the final output to only show the newly created url\_host column.
5. The limit 1 stage ensures that only a single result is returned.

**Output**:

| url\_host                       |
| ------------------------------- |
| "www.test.paloaltonetworks.com" |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`limit`](../stages/limit)
* **Functions**: [`extract_url_pub_suffix`](extract_url_pub_suffix), [`extract_url_registered_domain`](extract_url_registered_domain)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
