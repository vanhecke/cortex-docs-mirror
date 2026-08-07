# md5

Use the `md5()` function to compute the MD5 (Message-Digest Algorithm 5) hash of an input string.

## Syntax

```sql
md5 ("<input_string>")
```

## Parameters

| Name           | Type   | Required | Description              |
| -------------- | ------ | -------- | ------------------------ |
| `input_string` | string | Yes      | The string to be hashed. |

## Returns

The `md5()` function returns the MD5 hash value as a string.

## Usage notes

* The function strictly requires a single string input.
* MD5 is a one-way cryptographic hash function, meaning it is computationally infeasible to reverse the hashing process to obtain the original string from its hash.

## Examples

### Example 1: Hashing a basic literal string

**Goal**: Compute the MD5 hash of a simple literal string.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_string = md5("Hello world")
| fields event_id, hashed_string
| limit 3
```

**Explanation**: This query adds a new field, `hashed_string`, which contains the MD5 hash of "Hello world" for each record.

**Output**:

| EVENT\_ID | HASHED\_STRING                   |
| --------- | -------------------------------- |
| 101       | 3e25960a79dbc69b674cd4ec67a72c65 |
| 102       | 3e25960a79dbc69b674cd4ec67a72c65 |
| 103       | 3e25960a79dbc69b674cd4ec67a72c65 |

### Example 2: Hashing an existing string field

**Goal**: Hash values from an existing string field from the dataset.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_description = md5(event_description)
| fields event_id, event_description, hashed_description
| limit 3
```

**Explanation**: The query creates `hashed_description` by applying the `md5()` function to the `event_description` for each record.

**Output**:

| EVENT\_ID | EVENT\_DESCRIPTION             | HASHED\_DESCRIPTION              |
| --------- | ------------------------------ | -------------------------------- |
| 101       | User login successful          | e7751c911ee0541703e8787729227f2f |
| 102       | File access attempt            | be2254e015ee6b158055c56c2e28a506 |
| 103       | Network connection established | 24b74f0c43666f272a85e13b06385a86 |

### Example 3: Hashing a string derived from a non-string field

**Goal**: Convert a numeric field to a string and then hash it.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter event_id_string = to_string(event_id)
| alter hashed_id = md5(event_id_string)
| fields event_id, event_id_string, hashed_id
| limit 3
```

**Explanation**: The `event_id` is first converted to a string, and then `md5()` hashes this string representation.

**Output**:

| EVENT\_ID | EVENT\_ID\_STRING | HASHED\_ID                       |
| --------- | ----------------- | -------------------------------- |
| 101       | 101               | b16f6b0f199be0c27271457193f5509a |
| 102       | 102               | 00d720d2a8b233c4424316d764491024 |
| 103       | 103               | 19842c38f4d9b40778c1a9386d3d4b68 |

### Example 4: Hashing an empty string

**Goal**: Show the consistent result of hashing an empty string.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_empty_string = md5("")
| fields event_id, hashed_empty_string
| limit 3
```

**Explanation**: Hashing an empty string consistently results in the well-known MD5 hash for an empty string.

**Output**:

| EVENT\_ID | HASHED\_EMPTY\_STRING            |
| --------- | -------------------------------- |
| 101       | d41d8cd98f00b204e9800998ecf8427e |
| 102       | d41d8cd98f00b204e9800998ecf8427e |
| 103       | d41d8cd98f00b204e9800998ecf8427e |

### Example 5: Handling NULL input

**Goal**: Illustrate the function's behavior when provided with a NULL input.

**XQL code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter hashed_null_field = md5(dst_domain)
| fields event_id, dst_domain, hashed_null_field
| limit 5
```

**Explanation**: When the input to `md5()` is NULL, the function consistently returns NULL for the output field.

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
* **Functions**: [`sha1`](sha1), [`sha256`](sha256), [`sha512`](sha512)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
