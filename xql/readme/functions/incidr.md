# incidr

Use the `incidr()` function to determine if an IPv4 address is contained within one or more specified Classless Inter-Domain Routing (CIDR) blocks. The function returns `true` if the address falls within _any_ of the defined ranges, and `false` otherwise.

## Syntax

```sql
incidr (<ipv4_address_field>, "<cidr_range1>[, <cidr_range2>...]")
```

## Parameters

| Name                 | Type   | Required | Description                                                                                                                |
| -------------------- | ------ | -------- | -------------------------------------------------------------------------------------------------------------------------- |
| `ipv4_address_field` | string | Yes      | The field containing the IPv4 address (or a string literal) to evaluate.                                                   |
| `cidr_ranges`        | string | Yes      | A string literal containing one or more IPv4 ranges in CIDR notation (for example, "192.168.1.0/24"), separated by commas. |

## Returns

The `incidr()` function returns a boolean value (`true` or `false`).

## Usage notes

* The first parameter must contain an IPv4 address contained in an IPv4 field. For production purposes, this IPv4 address will normally be carried in a field that you retrieve from a dataset. For manual usage, assign the IPv4 address to a field, and then use that field with this function.
* This function is specifically designed for IPv4 addresses. For IPv6, use the `incidr6()` function.
* You can define multiple CIDR ranges within the second parameter string by separating them with commas.
* When multiple CIDR ranges are provided, the function uses logical **OR** logic. If the IP address falls within _any_ of the specified ranges, the function returns `true`.
* This function is commonly used within the `filter` stage to narrow down results based on network segments (for example, separating internal traffic from external traffic).
* To check if an IP is _not_ in a range, you can use the syntax `not incidr()`.

## Examples

### Example 1: Check if IP is in a single CIDR block (match)

**Goal**: Filter for records where the `ipv4_address` falls within a specific private network range (`192.168.1.0/24`).

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter ipv4_address incidr("192.168.1.0/24") 
| fields event_id, ipv4_address 
| limit 5 
```

**Explanation**: The query evaluates the `ipv4_address` for each record. The query returns the record with `event_id` 101 because its IP (`192.168.1.10`) is within the `192.168.1.0/24` range.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS |
| --------- | ------------- |
| 101       | 192.168.1.10  |

### Example 2: Check if IP is in a single CIDR block (no match)

**Goal**: Filter for records where the `ipv4_address` falls within the `10.0.0.0/8` private network range.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter ipv4_address incidr("10.0.0.0/8") 
| fields event_id, ipv4_address 
| limit 5 
```

**Explanation**: The query checks if the `ipv4_address` is in the `10.0.0.0/8` range. The query returns `event_id` 102 because its IP (`10.0.0.5`) falls within this block. Other records with different IPs (like 192.168.x.x) are excluded.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS |
| --------- | ------------- |
| 102       | 10.0.0.5      |

### Example 3: Check if IP address is in multiple CIDR blocks (logical OR)

**Goal**: Filter for records where the `ipv4_address` falls within _either_ the `10.0.0.0/8` range _or_ the `192.168.1.0/24` range.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter ipv4_address incidr("10.0.0.0/8, 192.168.1.0/24") 
| fields event_id, ipv4_address 
| limit 5 
```

**Explanation**: The query uses a comma-separated list of CIDRs. The query returns `event_id` 101 because `192.168.1.10` matches the second CIDR, and `event_id` 102 because `10.0.0.5` matches the first CIDR. This demonstrates the logical OR behavior.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS |
| --------- | ------------- |
| 101       | 192.168.1.10  |
| 102       | 10.0.0.5      |

### Example 4: Exclude IP addresses in multiple CIDR blocks (not incidr)

**Goal**: Filter for records where the `ipv4_address` does _not_ fall within common private IPv4 ranges, effectively filtering for public IPs.

**XQL code**:

```sql
config timeframe = 1d 
| dataset = sample_xql_raw 
| filter ipv4_address not incidr("10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16") 
| fields event_id, ipv4_address 
| limit 5 
```

**Explanation**: The query uses `not incidr` to exclude any IP addresses found in the specified private ranges. The query returns `event_id` 106 because its IP (`203.0.113.15`) is a public address and does not match any of the provided private CIDRs.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS |
| --------- | ------------- |
| 106       | 203.0.113.15  |

## Related articles

* **Stages**: [`filter`](../stages/filter)
* **Functions**: [`incidr6`](incidr6), [`incidrlist`](incidrlist)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
