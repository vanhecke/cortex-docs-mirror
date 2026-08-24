---
description: Query Windows Event Log records for Cortex XSIAM.
---

# Query Windows Event Log records

When the XDR Collector forwards Windows Event Log records to Cortex XSIAM, the records are available in Cortex Query Language (XQL) through two datasets, depending on the event's source provider. Use the correct dataset and field for your query to ensure you find the expected data.

### Dataset selection

| Dataset                 | What it contains                                                                                                                 | Use it when…                                                                                                     |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `xdr_data`              | All Windows Event Log records collected by the XDR Collector, in an EDR-style schema.                                            | You want a single dataset that always contains every collected Windows event, regardless of the source provider. |
| `microsoft_windows_raw` | Windows Event Log records, parsed in raw schema. By default, some high-volume or specialized providers are excluded (see below). | You want events in the standard `microsoft_windows_raw` schema and you do not need the excluded providers.       |

### Providers excluded from microsoft\_windows\_raw

The default Windows parsing rule excludes the following providers from `microsoft_windows_raw` to avoid duplicating data already consumed by out-of-the-box content in `xdr_data`:

* AD FS Auditing
* Microsoft-Windows-Sysmon
* Microsoft-Antimalware-Scan-Interface
* Microsoft-Windows-DNSServer
* Microsoft-Windows-DNS-Server-Service

Events from these providers are still ingested and are always queryable from `xdr_data`. They will not appear in `microsoft_windows_raw` unless you override the default rule.

**To include excluded providers:** Select **Settings** → **Configurations** → **Data Management** → **Parsing Rules**, edit the rule for `vendor = microsoft`, `product = windows`, and remove the provider from the exclusion list.

{% hint style="success" %}
**Tip**

If you query `microsoft_windows_raw` for events from one of these providers and get zero results, this is expected. Query `xdr_data` instead.
{% endhint %}

**For example**

In this example the pack name is `Microsoft Windows Event Logs`.

```
[INGEST:vendor="microsoft", product="windows", target_dataset="microsoft_windows_raw", no_hit=drop]
filter to_string(time_created) ~= ".*\d{2}:\d{2}:\d{2}.*" AND provider_name not in ("Microsoft-Windows-Sysmon", "AD FS Auditing", "Microsoft-Antimalware-Scan-Interface","Microsoft-Windows-DNSServer", "Microsoft-Windows-DNS-Server-Service")
| alter
    tmp_get_time = to_epoch(_time),
    tmp_get_insert_time = to_epoch(_insert_time),
    tmp_get_time_created = to_epoch(parse_timestamp("%FT%H:%M:%E*SZ",to_string(time_created)))
| alter
    _time = if(subtract(tmp_get_time_created, tmp_get_time) < 0, to_timestamp(tmp_get_time_created), subtract(tmp_get_insert_time, tmp_get_time) < 0, to_timestamp(tmp_get_insert_time), to_timestamp(tmp_get_time))
| alter
    _scope = coalesce(_scope, event_data -> _scope, event_data -> scope)
| fields -tmp*;
```

### Field Mapping in xdr\_data

When querying Windows Event Log records in `xdr_data`, use the following fields. The most common pitfall is using `event_id` to filter by Windows EventID; in `xdr_data`, this field is an internal identifier.

{% hint style="warning" %}
**Important**

To filter by Windows EventID, always use `action_evtlog_event_id`.
{% endhint %}

| XQL Field in xdr\_data        | What it contains                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------- |
| `action_evtlog_event_id`      | **The Windows EventID** (such as, 501, 512, 4624, 400). Use this field when filtering by EventID. |
| `event_id`                    | Internal per-record identifier. **Do not use this to filter by EventID.**                         |
| `event_type`                  | `15` for all Windows Event Log records.                                                           |
| `event_sub_type`              | `11` for all Windows Event Log records.                                                           |
| `agent_hostname`              | Source machine hostname.                                                                          |
| `action_evtlog_provider_name` | Source provider name (e.g., AD FS Auditing, PowerShell).                                          |
| `action_evtlog_record_id`     | Windows Event Log `RecordNumber`.                                                                 |
| `action_evtlog_data_fields`   | JSON string containing original `EventData` key/value pairs.                                      |

### Example queries

**Find Windows EventID 501 from a specific host:**

```xql
dataset = xdr_data
| filter agent_hostname = "<hostname>"
and action_evtlog_event_id = 501
| fields _time, agent_hostname, action_evtlog_event_id, action_evtlog_provider_name, action_evtlog_record_id, action_evtlog_data_fields
| sort desc _time
| limit 50
```

**Find events from providers excluded from microsoft\_windows\_raw:**

```xql
dataset = xdr_data
| filter agent_hostname = "<hostname>"
and action_evtlog_provider_name in ("AD FS Auditing", "Microsoft-Windows-Sysmon")
and action_evtlog_event_id in (501, 512)
| fields _time, agent_hostname, action_evtlog_event_id, action_evtlog_provider_name, action_evtlog_data_fields
| sort desc _time
| limit 50
```

### Troubleshooting checklist

If you cannot find an expected Windows event:

1. **Confirm collection:** Query `xdr_data` filtered by `agent_hostname` and `action_evtlog_event_id`.
2. **Verify field usage:** Ensure you are filtering on `action_evtlog_event_id`, not `event_id`.
3. **Check dataset/provider match:** If querying `microsoft_windows_raw`, ensure the provider isn't in the exclusion list. If it is, switch to `xdr_data`.
4. **Check collector profile:** In **Windows Event Viewer**, check the **Log Name** property of the event. This exact string must be listed under `winlogbeat.event_logs:` in your collector profile.
