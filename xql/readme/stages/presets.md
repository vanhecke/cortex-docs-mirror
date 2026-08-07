# preset

Use the `preset` stage to specify a predefined collection of fields from the `xdr_data` dataset as your data source, optimized for analyzing specific types of network or endpoint activity.

## Syntax

```sql
preset = <preset_name>
```

## Parameters

| Name          | Type   | Required | Description                                                                                      |
| ------------- | ------ | -------- | ------------------------------------------------------------------------------------------------ |
| `preset_name` | string | Yes      | The specific name of the preset to query (for example, `authentication_story`, `network_story`). |

## Returns

The `preset` stage returns a result set containing events and fields specific to the defined preset schema. These presets are often subsets of the `xdr_data` dataset, pre-filtered and organized for specific use cases like authentication, network traffic, or file operations.

## Usage notes

* Presets act as predefined views or "stories" (for example, `authentication_story`, `network_story`) that combine events and logs into a common schema.
* While presets offer convenience by pre-grouping fields, `XQL Query Optimization Principles` advise that for specific use cases, directly querying `dataset=xdr_data` with explicit filters (for example, `filter event_type = ...`) can often lead to better performance.
* General presets are designed for "well decorated, de-duplicated" results and may not prioritize performance impact; overly broad queries using presets can exceed optimization limits.
* To optimize performance when using presets (or their raw dataset alternatives), always apply `filter` stages as early as possible and use the `fields` stage to select only the necessary columns.

## Examples

### Example 1: Authentication story preset

**Goal**: Analyze authentication events using the `authentication_story` preset.

**XQL code**:

```sql
config timeframe = 7d
| preset = authentication_story
| fields agent_hostname, os_actor_effective_username, action_local_ip
| limit 10
```

**Explanation**: This query uses the `authentication_story` preset to focus on authentication logs, stitching together relevant information into a common schema. An optimized alternative would be querying `dataset = xdr_data` and filtering by `dfe_labels = "authentication"`.

**Output**:

| AGENT\_HOSTNAME | OS\_ACTOR\_EFFECTIVE\_USERNAME | ACTION\_LOCAL\_IP |
| --------------- | ------------------------------ | ----------------- |
| WORKSTATION-01  | jdoe                           | 192.168.1.15      |
| SERVER-DB-02    | admin                          | 10.0.0.50         |
| WORKSTATION-03  | asmith                         | 192.168.1.20      |

### Example 2: Network story preset

**Goal**: Aggregate network activity information using the `network_story` preset.

**XQL code**:

```sql
config timeframe = 7d
| preset = network_story
| filter action_remote_port = 443
| fields agent_hostname, action_local_ip, action_remote_ip, action_remote_port
| limit 10
```

**Explanation**: This query utilizes the `network_story` preset to provide a common schema for network events and filters specifically for HTTPS traffic (port 443). An optimized alternative involves querying `dataset = xdr_data` with `filter event_type = NETWORK`.

**Output**:

| AGENT\_HOSTNAME | ACTION\_LOCAL\_IP | ACTION\_REMOTE\_IP | ACTION\_REMOTE\_PORT |
| --------------- | ----------------- | ------------------ | -------------------- |
| HOST-A          | 10.10.10.5        | 172.217.16.14      | 443                  |
| HOST-B          | 10.10.10.8        | 142.250.185.78     | 443                  |
| HOST-C          | 10.10.10.12       | 204.79.197.200     | 443                  |

### Example 3: XDR event log preset

**Goal**: Analyze forensic event log data using the `xdr_event_log` preset.

**XQL code**:

```sql
config timeframe = 30d
| preset = xdr_event_log
| filter EVTX_Event_ID = 104
| fields host_name, Timestamp, message, EVTX_Event_ID
| limit 10
```

**Explanation**: This query uses the `xdr_event_log` preset to normalize and view event logs, specifically filtering for Windows System Event ID 104 (Log cleared). An optimized alternative would query `dataset = xdr_data` filtering for `event_type = ENUM.EVENT_LOG`.

**Output**:

| HOST\_NAME | TIMESTAMP     | MESSAGE                          | EVTX\_EVENT\_ID |
| ---------- | ------------- | -------------------------------- | --------------- |
| DC-01      | 1698304800000 | The System log file was cleared. | 104             |
| DC-02      | 1698305130000 | The System log file was cleared. | 104             |

### Example 4: XDR file preset

**Goal**: Investigate file-related events such as writes or accesses using the `xdr_file` preset.

**XQL code**:

```sql
config timeframe = 7d
| preset = xdr_file
| filter action_file_extension = "exe"
| fields event_id, action_file_name, action_file_path
| limit 10
```

**Explanation**: This query uses the `xdr_file` preset to focus on file activities, filtering specifically for executable files. An optimized alternative involves querying `dataset = xdr_data` with `filter event_type = ENUM.FILE`.

**Output**:

| EVENT\_ID | ACTION\_FILE\_NAME | ACTION\_FILE\_PATH          |
| --------- | ------------------ | --------------------------- |
| ev\_101   | update.exe         | C:\Temp\update.exe          |
| ev\_102   | malware.exe        | C:\Users\Public\malware.exe |

### Example 5: Host inventory users preset

**Goal**: Retrieve information about users discovered on endpoints using the `host_inventory_users` preset.

**XQL code**:

```sql
config timeframe = 30d
| preset = host_inventory_users
| filter disabled = true
| fields endpoint_name, name, full_name, disabled
| limit 10
```

**Explanation**: This query leverages the `host_inventory_users` preset (requiring Host Insights) to identify disabled user accounts on endpoints.

**Output**:

| ENDPOINT\_NAME | NAME       | FULL\_NAME        | DISABLED |
| -------------- | ---------- | ----------------- | -------- |
| LAPTOP-55      | Guest      | Guest User        | true     |
| SERVER-01      | old\_admin | Old Administrator | true     |

### Example 6: Host inventory shares preset

**Goal**: View details about shared resources on hosts using the `host_inventory_shares` preset.

**XQL code**:

```sql
config case_sensitive = false timeframe = 30d
| preset = host_inventory_shares
| filter description not contains "print"
| fields endpoint_name, description, share_type
| limit 5
```

**Explanation**: This query uses the `host_inventory_shares` preset to list shared resources, filtering out print shares to focus on other types of shares.

**Output**:

| ENDPOINT\_NAME | DESCRIPTION   | SHARE\_TYPE |
| -------------- | ------------- | ----------- |
| FILE-SERVER    | Finance Docs  | Disk        |
| BACKUP-SRV     | Daily Backups | Disk        |

### Example 7: Host users to groups preset

**Goal**: Analyze user-to-group mappings using the `host_users_to_groups` preset.

**XQL code**:

```sql
config case_sensitive = false timeframe = 30d
| preset = host_users_to_groups
| fields endpoint_name, user_name, group_name
| limit 5
```

**Explanation**: This query uses the `host_users_to_groups` preset (derived from Host Insights) to view the relationships between users and groups on endpoints.

**Output**:

| ENDPOINT\_NAME | USER\_NAME | GROUP\_NAME          |
| -------------- | ---------- | -------------------- |
| WORKSTATION-A  | alice      | Administrators       |
| WORKSTATION-A  | alice      | Remote Desktop Users |

### Example 8: Device control preset

**Goal**: Monitor USB device connections using the `device_control` preset.

**XQL code**:

```sql
config timeframe = 7d
| preset = device_control
| filter action_device_type = "USB"
| fields agent_hostname, action_device_id, action_device_info
| limit 10
```

**Explanation**: This query utilizes the `device_control` preset to view events related to USB device connections and disconnections.

**Output**:

| AGENT\_HOSTNAME | ACTION\_DEVICE\_ID       | ACTION\_DEVICE\_INFO  |
| --------------- | ------------------------ | --------------------- |
| USER-PC-01      | USB\VID\_0781\&PID\_5581 | SanDisk Ultra         |
| LAB-PC-04       | USB\VID\_0951\&PID\_1666 | Kingston DataTraveler |

## Related articles

* **Stages**: [`dataset`](dataset), [`filter`](filter), [`fields`](fields)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
