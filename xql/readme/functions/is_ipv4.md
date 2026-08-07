# is\_ipv4

Use the `is_ipv4()` function to determine if a string value represents a valid IPv4 address.

## Syntax

```sql
is_ipv4(<string>)
```

## Parameters

| Name     | Type   | Required | Description                                                      |
| -------- | ------ | -------- | ---------------------------------------------------------------- |
| `string` | string | Yes      | The string field or literal value to evaluate for IPv4 validity. |

## Returns

The `is_ipv4()` function returns a boolean value: true if the string is a valid IPv4 address, and false otherwise.

## Usage Notes

The function expects a string input and will return NULL if the input field is NULL.

Validation is strictly for IPv4 dotted-decimal format (for example, "192.168.1.1").

This function is typically used within the `alter` stage to tag records or within the filter stage to isolate specific traffic types.

## Examples

### Example 1: Validate IPv4 Addresses in a Dataset

**Goal**: Identify which records in the dataset contain a valid IPv4 address in the ipv4\_address field.

**XQL Code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| alter valid_ip = is_ipv4(ipv4_address)
| fields event_id, ipv4_address, valid_ip
| limit 3
```

**Explanation**: You use the is\_ipv4() function to check the `ipv4_address` field. For record 101, the `is_ipv4()` function returns true because "192.168.1.10" is a valid IPv4 address. For record 103, where the field is NULL, the `is_ipv4()` function returns NULL.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS | VALID\_IP |
| --------- | ------------- | --------- |
| 101       | 192.168.1.10  | true      |
| 102       | 10.0.0.5      | true      |
| 103       | NULL          | NULL      |

### Example 2: Filtering for Valid IPv4 Traffic

**Goal**: Filter the result set to return only those records that have a valid IPv4 address.

**XQL Code**:

```sql
config timeframe = 1d
| dataset = sample_xql_raw
| filter is_ipv4(ipv4_address) = true
| fields event_id, ipv4_address
| limit 2
```

**Explanation**: You apply the `is_ipv4()` function directly within a filter stage to exclude any records where the ipv4\_address field does not contain a properly formatted IPv4 address.

**Output**:

| EVENT\_ID | IPV4\_ADDRESS |
| --------- | ------------- |
| 101       | 192.168.1.10  |
| 102       | 10.0.0.5      |

## Related Articles

* **Stages**: [alter](../stages/alter), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [incidr()](incidr), [int\_to\_ip()](int_to_ip), [ip\_to\_int()](ip_to_int)
