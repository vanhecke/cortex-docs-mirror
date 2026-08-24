---
description: Use `parse_cisco` in Cortex XSIAM Parsing Rules.
---

# parse\_cisco

## **Syntax**

```programlisting
parse_cisco(<string>)
```

## **Description**

The `parse_cisco()` function processes a Cisco string and returns an object whose structure (key and value pairs) is determined by the input parameters. This function isn't available through the autocomplete when defining a user defined parsing rule. Yet, it is used in the parsing rule syntax for default parsing rules. Only a subset of Cisco ASA message types is supported as detailed in the Marketplace content pack.

## **Example**

This example shows how to parse a Cisco string called `_raw_log` into a JSON field called `_json` in a parsing rule.

Where the `_raw_log` field contains the following input:

```programlisting
<166>Apr 06 12:14:15 172.16.1.5 : %ASA-6-302014: Teardown TCP connection 1764964360 for TAP-Interface2:172.16.1.130/34206 to TAP-Interface:10.10.10.188/8000 duration 0:00:30 bytes 783 SYN Timeout
```

Updated \[INGEST] section in the parsing rule:

```programlisting
[INGEST:vendor="cisco", product="asa", target_dataset="cisco_asa_raw", no_hit = keep]
alter _json = parse_cisco(_raw_log)
| alter
        tmp_time = _json -> date
| alter
        _time = if(tmp_time contains "Z", parse_timestamp("%Y-%m-%dT%H:%M:%SZ", tmp_time), tmp_time ~= "[+-]\d{1,2}:\d{1,2}", parse_timestamp("%Y-%m-%dT%H:%M:%S%Ez", tmp_time))
| fields - tmp_time;
```

Where the `_json` field contains the following output:

```programlisting
{
    "severity": "informational",
    "logType": "302014",
    "date": "2026-04-06T12:14:15Z",
    "device": "172.16.1.5",
    "action": "teardown",
    "protocol": "TCP",
    "inOutBound": "unknown",
    "connectionId": "1764964360",
    "durationSeconds": 30,
    "sentBytes": 783,
    "to":
    {
        "interface": "TAP-Interface",
        "address": "10.10.10.188",
        "port": 8000
    },
    "from":
    {
        "interface": "TAP-Interface2",
        "address": "172.16.1.130",
        "port": 34206
    },
    "generalCiscoLog":
    {
        "action": "Teardown",
        "protocol": "TCP",
        "src_ip": "172.16.1.130",
        "src_port": "34206",
        "dst_ip": "10.10.10.188",
        "dst_port": "8000",
        "src_interface": "TAP-Interface2",
        "dst_interface": "TAP-Interface",
        "src_mapped_ip": "",
        "src_mapped_port": "",
        "duration": "0:00:30",
        "transferred_bytes": "783"
    }
}
```
