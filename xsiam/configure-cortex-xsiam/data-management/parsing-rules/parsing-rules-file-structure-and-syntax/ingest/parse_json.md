# parse\_json

## Syntax

```
parse_json()
```

## Description

The `parse_json()` function processes a JSON string and returns an object whose structure (key and\
value pairs) is determined by the input parameters.

## Example

This example parses a JSON string to return a key and value pairs object based on the input parameters.

```
dataset = xdr_data
| alter json_string = "{'a':'b'}"
| alter result = parse_json(json_string)
| fields result
```

### Output results

The results return an object with key 'a' having value 'b'.
