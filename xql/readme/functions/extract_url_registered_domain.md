# extract\_url\_registered\_domain

Use the `extract_url_registered_domain()` function to retrieve the registered domain (also known as the registerable domain) from a URL string. This typically consists of the public suffix plus one preceding label (for example, extracting `paloaltonetworks.com` from `www.paloaltonetworks.com`).

## Syntax

```sql
extract_url_registered_domain ("<URL>")
```

## Parameters

| Name    | Type   | Required | Description                                                                                         |
| ------- | ------ | -------- | --------------------------------------------------------------------------------------------------- |
| `<URL>` | string | Yes      | The input string literal or field containing the URL from which the registered domain is extracted. |

## Returns

The `extract_url_registered_domain()` function returns a string representing the registered domain of the URL.

## Usage notes

* The function accepts a string value representing a URL as input.
* The function always returns the registered domain value in lowercase characters, regardless of the casing in the input URL.
* If the input URL structure does not contain a recognizable registered domain (such as a private IP address or a malformed URL), the function returns `NULL`.
* If the input value is `NULL`, the function returns `NULL`.

## Examples

### Example 1: Basic registered domain extraction from a standard URL

**Goal**: Extract the registered domain from a standard HTTPS URL.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter extracted_registered_domain = extract_url_registered_domain("https://www.paloaltonetworks.com")
| fields event_id, extracted_registered_domain
| limit 1
```

**Explanation**: The query extracts "paloaltonetworks.com" as the registered domain from the URL "https://www.paloaltonetworks.com".

**Output**:

| EVENT\_ID | EXTRACTED\_REGISTERED\_DOMAIN |
| --------- | ----------------------------- |
| 101       | paloaltonetworks.com          |

### Example 2: Registered domain extraction from a URL with multiple subdomains/paths

**Goal**: Extract the registered domain from a URL that includes multiple subdomains and extended path components.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter extracted_registered_domain_complex = extract_url_registered_domain("https://docs.global.paloaltonetworks.com/xql/api")
| fields event_id, extracted_registered_domain_complex
| limit 1
```

**Explanation**: The function correctly isolates "paloaltonetworks.com" as the registered domain, ignoring the "docs.global" subdomains and the "/xql/api" path components.

**Output**:

| EVENT\_ID | EXTRACTED\_REGISTERED\_DOMAIN\_COMPLEX |
| --------- | -------------------------------------- |
| 101       | paloaltonetworks.com                   |

### Example 3: Registered domain extraction with mixed-case input

**Goal**: Extract the registered domain from a URL containing uppercase letters to demonstrate automatic lowercasing.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter extracted_registered_domain_lowercase = extract_url_registered_domain("WWW.EXAMPLE.Co.UK/docs")
| fields event_id, extracted_registered_domain_lowercase
| limit 1
```

**Explanation**: Despite the input "WWW.EXAMPLE.Co.UK/docs" having mixed casing, the function returns the registered domain "example.co.uk" in all lowercase characters.

**Output**:

| EVENT\_ID | EXTRACTED\_REGISTERED\_DOMAIN\_LOWERCASE |
| --------- | ---------------------------------------- |
| 101       | example.co.uk                            |

### Example 4: Handling URLs without a recognizable registered domain

**Goal**: Demonstrate the function's behavior when provided with inputs that do not represent a recognizable registered domain, such as malformed URLs or private IP addresses.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter invalid_url_registered_domain = extract_url_registered_domain("//user:password@a.b:80/path?query")
| alter private_ip_registered_domain = extract_url_registered_domain("192.168.1.10")
| fields event_id, invalid_url_registered_domain, private_ip_registered_domain
| limit 1
```

**Explanation**: For the malformed URL and the private IP address "192.168.1.10", the function cannot determine a registered domain and returns `NULL`.

**Output**:

| EVENT\_ID | INVALID\_URL\_REGISTERED\_DOMAIN | PRIVATE\_IP\_REGISTERED\_DOMAIN |
| --------- | -------------------------------- | ------------------------------- |
| 101       | NULL                             | NULL                            |

### Example 5: Handling NULL input

**Goal**: Demonstrate the behavior when the input field is `NULL`.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter event_id = 105
| alter extracted_registered_domain_from_null = extract_url_registered_domain(dst_domain)
| fields event_id, dst_domain, extracted_registered_domain_from_null
| limit 1
```

**Explanation**: The `dst_domain` field is `NULL` for event 105. Consistent with standard XQL function behavior, the function returns `NULL`.

**Output**:

| EVENT\_ID | DST\_DOMAIN | EXTRACTED\_REGISTERED\_DOMAIN\_FROM\_NULL |
| --------- | ----------- | ----------------------------------------- |
| 105       | NULL        | NULL                                      |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`filter`](../stages/filter), [`limit`](../stages/limit)
* **Functions**: [`extract_url_host`](extract_url_host), [`extract_url_pub_suffix`](extract_url_pub_suffix)
