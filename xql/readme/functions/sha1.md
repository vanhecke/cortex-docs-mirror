# sha1

Use the `sha1()` function to compute the SHA-1 (Secure Hash Algorithm 1) hash of an input string.

## Syntax

```sql
sha1 ("<input_string>")
```

## Parameters

| Name           | Type   | Required | Description              |
| -------------- | ------ | -------- | ------------------------ |
| `input_string` | string | Yes      | The string to be hashed. |

## Returns

The `sha1()` function returns the SHA-1 hash value as a string.

## Usage notes

* The function strictly requires a single string input.
* SHA-1 is a one-way cryptographic hash function, meaning it is computationally infeasible to reverse the hashing process to obtain the original string from its hash.
* To hash values from non-string fields (such as integers or booleans), you must first convert them to a string using the `to_string()` function.

## Examples

### Example 1: Hashing a basic literal string

**Goal**: Compute the SHA-1 hash of a simple literal string value.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_literal = sha1("Hello XQL!")
| fields event_id, hashed_literal
| limit 3
```

**Explanation**: This query adds a new field, `hashed_literal`, containing the SHA-1 hash of the string "Hello XQL!" for each record.

**Output**:

| EVENT\_ID | HASHED\_LITERAL                          |
| --------- | ---------------------------------------- |
| 101       | 6938947f6424594a11b6ff4f04c6439162e84d41 |
| 102       | 6938947f6424594a11b6ff4f04c6439162e84d41 |
| 103       | 6938947f6424594a11b6ff4f04c6439162e84d41 |

### Example 2: Hashing an existing string field

**Goal**: Compute the SHA-1 hash for values within an existing string field.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_description = sha1(event_description)
| fields event_id, event_description, hashed_description
| limit 3
```

**Explanation**: The query creates the `hashed_description` field by applying the `sha1()` function to the `event_description` field for each record.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             | HASHED\_DESCRIPTION              |
| --------- | ------------------------------ | -------------------------------- |
| 101       | User login successful          | e7751c911ee0541703e8787729227f2f |
| 102       | File access attempt            | be2254e015ee6b158055c56c2e28a506 |
| 103       | Network connection established | 24b74f0c43666f272a85e13b06385a86 |

### Example 3: Hashing a string derived from a non-string field

**Goal**: Convert a numeric field to a string and then compute its SHA-1 hash.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_string = to_string(event_id)
| alter hashed_id = sha1(event_id_string)
| fields event_id, event_id_string, hashed_id
| limit 3
```

**Explanation**: The `event_id` is first converted to a string using `to_string()`, and then `sha1()` hashes this string representation to create `hashed_id`.

**Output**:

| EVENT\_ID | EVENT\_ID\_STRING | HASHED\_ID                               |
| --------- | ----------------- | ---------------------------------------- |
| 101       | 101               | b00b7407519106093416e91122a6136e090f75f7 |
| 102       | 102               | 041c2c366ff4281f69201103f1673891404c0df2 |
| 103       | 103               | 1488c525f77876a3e5c709e3a35a7707e77a1024 |

### Example 4: Hashing an empty string

**Goal**: Demonstrate the result of hashing an empty string.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_empty_string = sha1("")
| fields event_id, hashed_empty_string
| limit 3
```

**Explanation**: Hashing an empty string consistently results in the well-known SHA-1 hash for an empty string.

**Output**:

| EVENT\_ID | HASHED\_EMPTY\_STRING                    |
| --------- | ---------------------------------------- |
| 101       | da39a3ee5e6b4b0d3255bfef95601890afd80709 |
| 102       | da39a3ee5e6b4b0d3255bfef95601890afd80709 |
| 103       | da39a3ee5e6b4b0d3255bfef95601890afd80709 |

### Example 5: Handling NULL input

**Goal**: Observe the behavior when the input to the function is NULL.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_null_field = sha1(dst_domain)
| fields event_id, dst_domain, hashed_null_field
| li
```

**Explanation**: When the input to `sha1()` is NULL (as seen in event 105), the function consistently returns NULL for the output field.

**Output**:

| EVENT\_ID | DST\_DOMAIN       | HASHED\_NULL\_FIELD              |
| --------- | ----------------- | -------------------------------- |
| 101       | ec2.amazonaws.com | 7f2f11181827457c134012019c4d93e5 |
| 102       | sts.amazonaws.com | fdf15a896d92008779b1248039601d0f |
| 103       | www.google.com    | 121f66cb71158f964092b3a1a36173a7 |
| 104       | dropbox.com       | 84b7a137e0c4573130d740a6b47c0b6b |
| 105       | NULL              | NULL                             |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`md5`](md5), [`sha256`](sha256), [`sha512`](sha512), [`to_string`](to_string)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
