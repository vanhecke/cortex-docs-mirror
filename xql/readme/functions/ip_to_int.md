# ip\_to\_int

Use the `ip_to_int()` function to safely convert a string representation of an IPv4 address into its signed integer equivalent.

## Syntax

```sql
ip_to_int (<IPv4_address>)
```

## Parameters

| Name           | Type   | Required | Description                                        |
| -------------- | ------ | -------- | -------------------------------------------------- |
| `IPv4_address` | string | Yes      | The string representation of a valid IPv4 address. |

## Returns

The `ip_to_int()` function returns the signed integer representation of the provided IPv4 address string.

## Usage notes

* This function is designed to safely convert a string representation of an IPv4 address into its signed integer equivalent.
* This conversion is crucial for scenarios where numerical operations or comparisons are required on IP addresses, or for storing them in an integer format.
* `ip_to_int()` is the inverse of `int_to_ip()`, which converts an integer representation of an IPv4 address back to its string format.
* This function was previously known as `safe_ip_to_int()`.
* If the input `IPv4_address` is `NULL`, the function returns `NULL`.

## Examples

### Example 1: Converting a literal IPv4 address string

**Goal**: Convert a static string representation of an IPv4 address into its integer form.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_ip_int = ip_to_int("48.49.50.51") // Converts the literal string "48.49.50.51" to an integer 
| fields event_id, converted_ip_int 
| limit 3 
```

**Explanation**: The query creates a new field `converted_ip_int` by converting the literal IPv4 string "48.49.50.51" to its integer equivalent, which is 808530483. This value is constant across all returned records.

**Output**:

| EVENT\_ID | CONVERTED\_IP\_INT |
| --------- | ------------------ |
| 101       | 808530483          |
| 102       | 808530483          |
| 103       | 808530483          |

### Example 2: Converting an IPv4 address from a dataset field

**Goal**: Apply the function to the `ipv4_address` field present in the dataset.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| alter converted_ip_from_field = ip_to_int(ipv4_address) // Converts the ipv4_address field to an integer 
| fields event_id, ipv4_address, converted_ip_from_field 
| limit 6 
```

**Explanation**: For each record, `ipv4_address` is converted to its integer representation in the `converted_ip_from_field`. Records with a `NULL` `ipv4_address` (like `event_id` 103) will also result in a `NULL` `converted_ip_from_field`.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS  | CONVERTED\_IP\_FROM\_FIELD |
| --------- | -------------- | -------------------------- |
| 101       | 192.168.1.10   | 3232235786                 |
| 102       | 10.0.0.5       | 167772165                  |
| 103       | NULL           | NULL                       |
| 104       | 172.31.255.255 | 2892780543                 |
| 105       | 192.168.10.20  | 3232238100                 |
| 106       | 203.0.113.15   | 3407889679                 |

### Example 3: Handling NULL input

**Goal**: Demonstrate behavior when provided with a `NULL` input, by filtering for records where `ipv4_address` is `NULL`.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter ipv4_address = null // Focus on records where ipv4_address is NULL 
| alter converted_null_ip_int = ip_to_int(ipv4_address) // Attempts conversion of NULL 
| fields event_id, ipv4_address, converted_null_ip_int 
| limit 3 
```

**Explanation**: As is standard behavior for XQL functions when encountering null inputs, `ip_to_int()` returns `NULL` when its input `ipv4_address` is `NULL`.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS | CONVERTED\_NULL\_IP\_INT |
| --------- | ------------- | ------------------------ |
| 103       | NULL          | NULL                     |
| 107       | NULL          | NULL                     |
| 109       | NULL          | NULL                     |

### Example 4: Converting a private IPv4 address

**Goal**: Target a specific private IPv4 address from the dataset to demonstrate its conversion.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 102 // Selects event with a private IP: 10.0.0.5 
| alter private_ip_as_int = ip_to_int(ipv4_address) // Converts the private IPv4 string to integer 
| fields event_id, ipv4_address, private_ip_as_int 
| limit 1 
```

**Explanation**: The private IP address "10.0.0.5" is successfully converted to its corresponding integer value 167772165.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS | PRIVATE\_IP\_AS\_INT |
| --------- | ------------- | -------------------- |
| 102       | 10.0.0.5      | 167772165            |

### Example 5: Converting a public IPv4 address

**Goal**: Target a specific public IPv4 address from the dataset to demonstrate its conversion.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter event_id = 106 // Selects event with a public IP: 203.0.113.15 
| alter public_ip_as_int = ip_to_int(ipv4_address) // Converts the public IPv4 string to integer 
| fields event_id, ipv4_address, public_ip_as_int 
| limit 1 
```

**Explanation**: The public IP address "203.0.113.15" is successfully converted to its corresponding integer value 3407889679.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS | PUBLIC\_IP\_AS\_INT |
| --------- | ------------- | ------------------- |
| 106       | 203.0.113.15  | 3407889679          |

## Related articles

* **Stages**: [`alter`](../stages/alter), [`config`](../stages/config), [`fields`](../stages/fields), [`filter`](../stages/filter), [`limit`](../stages/limit)
* **Functions**: [`int_to_ip`](int_to_ip)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
