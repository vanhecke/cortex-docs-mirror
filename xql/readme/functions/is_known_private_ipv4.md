# is\_known\_private\_ipv4

Use the `is_known_private_ipv4()` function to determine if a string value represents a known private, non-routable IPv4 address.

## Syntax

```sql
is_known_private_ipv4(<string>)
```

## Parameters

| Name   | Type   | Required | Description                                                                 |
| ------ | ------ | -------- | --------------------------------------------------------------------------- |
| string | string | Yes      | The string field or literal value representing an IPv4 address to evaluate. |

## Returns

The `is_known_private_ipv4()` function returns a boolean value `true` if the string is a valid private IPv4 address (such as those defined in RFC 1918), and `false` otherwise.

## Usage Notes

* The function expects a string input and returns `NULL` if the input field is `NULL` or does not evaluate to a valid IPv4 address.
* The function evaluates standard private and special-purpose IP address spaces, typically including 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, loopback addresses (127.0.0.0/8), and link-local addresses (169.254.0.0/16).
* This function is frequently used within the `alter` stage to tag internal network traffic, or within the `filter` stage to exclude internal communication from external threat hunts.

## Examples

### Example 1: Identify Private IPv4 Addresses in a Dataset

**Goal**: Identify which records in the dataset contain a known private IPv4 address in the `ipv4_address` field.

**XQL Code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter is_private = is_known_private_ipv4(ipv4_address)
| fields event_id, ipv4_address, is_private
| limit 3

```

**Explanation**: You use the `is_known_private_ipv4()` function to check the `ipv4_address` field. For record 101, the function returns `true` because "10.0.0.5" belongs to a private subnet. For record 102, it returns `false` because "8.8.8.8" is a public routable IP. For record 103, where the field is `NULL`, it returns `NULL`.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS | IS\_PRIVATE |
| --------- | ------------- | ----------- |
| 101       | 10.0.0.5      | true        |
| 102       | 8.8.8.8       | false       |
| 103       | NULL          | NULL        |

### Example 2: Filtering for External (Public) IPv4 Traffic

**Goal**: Filter the result set to return only those records that do _not_ contain a private IPv4 address.

**XQL Code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter is_known_private_ipv4(ipv4_address) = false
| fields event_id, ipv4_address
| limit 2

```

**Explanation**: You apply the `is_known_private_ipv4()` function directly within a filter stage and check for `false` to isolate external (public) IP addresses, filtering out any internal traffic.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS |
| --------- | ------------- |
| 102       | 8.8.8.8       |
| 104       | 1.1.1.1       |

## Related Articles

* **Stages**: [alter](../stages/alter), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [is\_ipv4()](is_ipv4), [is\_ipv6()](is_ipv6), [incidr()](incidr)
