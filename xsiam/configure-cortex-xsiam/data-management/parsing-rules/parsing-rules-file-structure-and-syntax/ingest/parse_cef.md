# parse\_cef

## Syntax

```
parse_cef()
```

## Description

The `parse_cef()` function processes a CEF string and returns an object whose structure (key and\
value pairs) is determined by the input parameters.

## Example: Parsing CEF logs during ingestion

The following example demonstrates how to use the `parse_cef` function within a parsing rule to process raw logs and store the resulting object in a specific dataset. This logic is configured in the `INGEST` section to execute as data is written to Cortex XSIAM.

```
[INGEST:vendor="test", product="parse_cef", target_dataset="test_parse_cef_raw", no_hit = keep]
alter raw ="<14>Oct  2 10:06:18 PAN-PROD-APPSVC-EU-W4-FW01 CEF:0|Palo Alto Networks|PAN-OS|8.1.15-h3|end|TRAFFIC|1|rt=Oct 02 2022 17:06:18 GMT src=35.204.254.72 app=ssl proto=TCP in=8697 double=1.15 mac=B3-F5-10-ED-C4-EE ad.vd=root ad.subtype=forward pattern:test=test"
| alter parsed = parse_cef(raw)
| fields parsed;
```

### Explanation of the rule components:

* `INGEST` section: Defines the `vendor`, `product`, and the `target_dataset` where the parsed logs will be stored.
* `alter raw`: In this rule context, this defines the source string to be parsed (simulating the `_raw_log` input).
* `parse_cef(raw)`: Processes the CEF string into a structured object containing key-value pairs.
* Semicolon (`;`): Required at the end of the rule to ensure proper compilation.

## Output results

The following JSON represents the structured object stored in the parsed field of the `test_parse_cef_raw` dataset after the rule is applied:<br>

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
