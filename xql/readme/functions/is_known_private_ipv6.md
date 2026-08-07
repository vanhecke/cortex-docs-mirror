# is\_known\_private\_ipv6

Use the `is_known_private_ipv6()` function to determine if a string value represents a known private, non-routable IPv6 address.

## Syntax

```xql
is_known_private_ipv6(\<string\>)
```

## Parameters

| Name   | Type   | Required | Description                                                                 |
| ------ | ------ | -------- | --------------------------------------------------------------------------- |
| string | string | Yes      | The string field or literal value representing an IPv6 address to evaluate. |

## Returns

The `is_known_private_ipv6()` function returns a boolean value: true if the string is a valid private IPv6 address (such as those defined in RFC 4193 for Unique Local Addresses), and false otherwise.

## Usage Notes

* The function expects a string input and will return NULL if the input field is NULL or does not evaluate to a valid IPv6 address.
* The function evaluates standard private and special-purpose IPv6 address spaces, typically including Unique Local Addresses (ULA) within the fc00::/7 block (which includes fd00::/8), loopback addresses (::1/128), and link-local addresses (fe80::/10).
* This function is frequently used within the alter stage to tag internal network traffic, or within the filter stage to exclude internal communication from external threat hunts.

## Examples

### Example 1: Identify Private IPv6 Addresses in a Dataset

**Goal**: Identify which records in the dataset contain a known private IPv6 address in the ip field.

**XQL Code**:

```xql
dataset = ips_test_raw
| alter is_private = is_known_private_ipv6(ip)
| fields _time, ip, is_private
| limit 3
```

**Explanation**: You use the `is_known_private_ipv6()` function in the alter stage to check the ip field. For the first record, the function returns true because fc00::1 is a Unique Local Address (ULA) and thus a private subnet. For the second record, it returns false because 2606:4700:4700::1111 is a public routable IPv6 address. For the third record, where the field is an IPv4 address, it returns NULL.

**Output**:

| **\_TIME**             | **IP**               | **IS\_PRIVATE** |
| ---------------------- | -------------------- | --------------- |
| Mar 26th 2025 19:26:07 | fc00::1              | true            |
| Mar 26th 2025 19:26:07 | 2606:4700:4700::1111 | false           |
| Mar 26th 2025 19:26:07 | 10.0.0.5             | NULL            |

### Example 2: Filtering for External (Public) IPv6 Traffic

**Goal**: Filter a dataset to return only those records that contain a valid IPv6 address that is _not_ a private address.

**XQL Code**:

```sql
dataset = ips_test_raw
| filter is_ipv6(ip) and is_known_private_ipv6(ip) = false
| fields _time, ip

```

**Explanation**: You apply both the `is_ipv6()` and `is_known_private_ipv6()` functions directly within a filter stage. By ensuring the address is a valid IPv6 format and checking for false on the private evaluation, you isolate external (public) IPv6 addresses, filtering out any internal traffic or standard IPv4 data.

**Output**:

| **\_TIME**             | **IP**                                 |
| ---------------------- | -------------------------------------- |
| Mar 26th 2025 19:26:07 | 2606:4700:4700::1111                   |
| Mar 26th 2025 19:26:07 | 2001:db8:3333:4444:5555:6666:7777:8888 |

## Related Articles

* **Stages**: [alter](../stages/alter), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [is\_ipv6()](is_ipv6), [is\_known\_private\_ipv4()](is_known_private_ipv4), [incidr6()](incidr6)
* **Datasets**: [ips\_test\_raw](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
