# int\_to\_ip

Use the `int_to_ip()` function to convert a signed integer representation of an IPv4 address into its standard dotted-decimal string equivalent.

## Syntax

```sql
int_to_ip(<IPv4_integer>)
```

## Parameters

| Name           | Type    | Required | Description                                        |
| -------------- | ------- | -------- | -------------------------------------------------- |
| `IPv4_integer` | integer | Yes      | The integer value that represents an IPv4 address. |

## Returns

The `int_to_ip()` function returns the corresponding IPv4 address as a string.

## Usage notes

* This function is the inverse of the `ip_to_int()` function, which converts a string representation of an IPv4 address to an integer.
* The function safely handles signed integers, meaning it can process both positive and negative integer inputs to produce valid IP address strings.
* Ideally, this function is utilized within the `alter` stage to create new fields or modify existing ones based on the converted IP address.

## Examples

### Example 1: Convert standard positive integer to IPv4

**Goal**: Convert a standard positive integer representing an IPv4 address to its dotted-decimal string form.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_ip = int_to_ip(75643532) 
| fields event_id, converted_ip 
| limit 3 
```

**Explanation**: The query creates a new field `converted_ip` by converting the integer `75643532` to its IPv4 string equivalent, which is "4.130.58.140".

**Output**:

| EVENT\_ID | CONVERTED\_IP |
| --------- | ------------- |
| 101       | 4.130.58.140  |
| 102       | 4.130.58.140  |
| 103       | 4.130.58.140  |

### Example 2: Convert negative integer to IPv4

**Goal**: Convert a negative integer, which represents an IPv4 address in a different byte order, to its corresponding dotted-decimal string.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_ip = int_to_ip(-75643532) 
| fields event_id, converted_ip 
| limit 3 
```

**Explanation**: The query creates a new field `converted_ip` by converting the integer `-75643532` to its IPv4 string equivalent, which is "251.125.197.116".

**Output**:

| EVENT\_ID | CONVERTED\_IP   |
| --------- | --------------- |
| 101       | 251.125.197.116 |
| 102       | 251.125.197.116 |
| 103       | 251.125.197.116 |

### Example 3: Convert zero to IPv4

**Goal**: Convert the integer 0 to its IPv4 address string representation.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_ip = int_to_ip(0) 
| fields event_id, converted_ip 
| limit 3 
```

**Explanation**: The query creates `converted_ip` by converting `0` to its IPv4 string equivalent, "0.0.0.0".

**Output**:

| EVENT\_ID | CONVERTED\_IP |
| --------- | ------------- |
| 101       | 0.0.0.0       |
| 102       | 0.0.0.0       |
| 103       | 0.0.0.0       |

### Example 4: Convert large positive integer to IPv4 (broadcast address)

**Goal**: Convert the maximum unsigned 32-bit integer to its IPv4 address string representation, which corresponds to the broadcast address.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_ip = int_to_ip(4294967295) // Converts the integer 4294967295 (2^32 - 1) to an IPv4 address
| fields event_id, converted_ip 
| limit 3 
```

**Explanation**: The query creates a new field `converted_ip` by converting the integer `4294967295` (which is ) to its IPv4 string equivalent, "255.255.255.255".

**Output**:

| EVENT\_ID | CONVERTED\_IP   |
| --------- | --------------- |
| 101       | 255.255.255.255 |
| 102       | 255.255.255.255 |
| 103       | 255.255.255.255 |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`ip_to_int`](ip_to_int)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
