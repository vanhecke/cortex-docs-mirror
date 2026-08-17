# parse\_cef

## Syntax

```
parse_cef()
```

## Description

The `parse_cef()` function processes a CEF string and returns an object whose structure (key and\
value pairs) is determined by the input parameters.

## Example

This example parses a CEF string to return a key and value pairs object based on the input parameters.

```
dataset = xdr_data
| alter raw ="<14>Oct  2 10:06:18 PAN-PROD-APPSVC-EU-W4-FW01 CEF:0|Palo Alto Networks|PAN-OS|8.1.15-h3|end|TRAFFIC|1|rt=Oct 02 2022 17:06:18 GMT src=35.204.254.72 app=ssl proto=TCP in=8697 double=1.15 mac=B3-F5-10-ED-C4-EE ad.vd=root ad.subtype=forward pattern:test=test"
| alter parsed = parse_cef(raw)
| fields parsed
```

### Output results

The results displayed is an object with the following contents:

```
"parsed": {
  "ad.subtype": "forward",
  "ad.vd": "root",
  "app": "ssl",
  "cefDeviceEventClassId": "end",
  "cefDeviceProduct": "PAN-OS",
  "cefDeviceVendor": "Palo Alto Networks",
  "cefDeviceVersion": "8.1.15-h3",
  "cefName": "TRAFFIC",
  "cefSeverity": "1",
  "cefVersion": "CEF:0",
  "double": "1.15",
  "in": "8697",
  "mac": "B3-F5-10-ED-C4-EE",
  "pattern:test": "test",
  "proto": "6",
  "rt": 1664730378000,
  "src": "35.204.254.72"
}
```
