# limit

Use the `limit` stage to explicitly set the upper bound for the number of records returned by an XQL query. This is crucial for optimizing query performance, reducing data processing volume, and minimizing memory usage for operations like sorting.

## Syntax

```sql
limit <number>
```

## Parameters

| Name       | Type    | Required | Description                                                |
| ---------- | ------- | -------- | ---------------------------------------------------------- |
| `<number>` | integer | Yes      | The maximum number of records to return in the result set. |

## Returns

The `limit` stage returns a subset of the input records, restricted to the maximum count specified by the `<number>` parameter.

## Usage notes

* Unless a `limit` stage is explicitly stated, standard XQL queries have a default maximum limit of 1,000,000 results.
* Basic XQL queries (and XDM queries in Cortex XSIAM) that contain no stages beyond a `fields` stage have a default limit of 1,000 results.
* The 1,000-result default limit for basic queries does not apply to widgets, Correlation Rules, public APIs, saved queries, or scheduled queries, which maintain the 1,000,000-result limit if unspecified.
* We recommend placing the `limit` stage after sorting (`sort`) to ensure you are retrieving the top or bottom records based on your criteria, rather than an arbitrary subset.
* Applying `limit` after filtering (`filter`) ensures that the limit applies only to the relevant records, optimizing data processing.

## Examples

### Example 1: Basic limit to restrict total records

**Goal**: Retrieve a specified number of records from the dataset without specific ordering or filtering.

**XQL code**:

```sql
dataset = sample_xql_raw
| limit 5
```

**Explanation**: This query returns the first 5 records found in the `sample_xql_raw` dataset. Since no sort order is defined, the records are returned in the order they appear in the source.

**Output**:

| event\_id | \_time                  | event\_description               | is\_successful | duration\_seconds | simple\_json\_data                                | nested\_json\_data                                                                                   | array\_of\_json\_objects                                                                                        | string\_tags                | numeric\_codes             | raw\_log\_data                                            | ipv4\_address    | ipv6\_address  |
| --------- | ----------------------- | -------------------------------- | -------------- | ----------------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------- | -------------------------- | --------------------------------------------------------- | ---------------- | -------------- |
| 101       | 2023-10-26 10:00:00 UTC | "User login successful"          | true           | 1.5               | {"status": "ok", "code": 200}                     | {"user": {"id": "U1", "name": "Alice"}, "session": {"start": "10:00", "type": "web"\}}               | \[{"action": "read", "file": "doc1.txt"}, {"action": "write", "file": "report.log"}]                            | \["security", "login"]      | \[13, -47, 29, 82, -15]    | "User Alice logged in from 192.168.1.10"                  | "192.168.1.10"   | NULL           |
| 102       | 2023-10-26 10:05:30 UTC | "File access attempt"            | false          | 0.8               | {"status": "fail", "error": "access\_denied"}     | {"process": {"name": "cmd.exe", "pid": 1234}, "target": {"path": "/var/log", "permission": "rwx"\}}  | \[{"event": "file\_open", "path": "/etc/passwd"}]                                                               | \["filesystem", "critical"] | \[-21, 56, 13, -88, 42]    | "Process cmd.exe attempted to access /etc/passwd"         | "10.0.0.5"       | NULL           |
| 103       | 2023-10-26 10:15:15 UTC | "Network connection established" | true           | 10.2              | {"connection\_id": "CONN-001", "protocol": "TCP"} | {"source": {"ip": "172.16.0.1", "port": 5000}, "destination": {"ip": "1.1.1.1", "port": 443\}}       | \[{"conn\_type": "outbound", "bytes": 1024}, {"conn\_type": "inbound", "bytes": 512}]                           | \["network", "cloud"]       | \[90, -33, 7, 51, -62, 18] | "Outbound connection to 1.1.1.1:443 initiated by AppX"    | NULL             | "2001:0db8::1" |
| 104       | 2023-10-26 10:20:00 UTC | "System heartbeat"               | true           | 0.1               | {"health": "good"}                                | {"system": {"cpu\_util": 0.15, "mem\_free": "80%"}, "status": "active"}                              | \[]                                                                                                             | \["monitoring"]             | \[]                        | "System health check passed"                              | "172.31.255.255" | NULL           |
| 105       | 2023-10-26 10:30:45 UTC | "Data transformation"            | true           | 5.0               | {"transform\_stage": 1}                           | {"pipeline": {"id": "P5", "status": "running"}, "data": {"records\_in": 1000, "records\_out": 950\}} | \[{"step": "parse", "time\_ms": 100}, {"step": "filter", "time\_ms": 200}, {"step": "enrich", "time\_ms": 300}] | \["data\_ops"]              | \[77, -9, 35, -47, 61]     | "Transformed data from source X, processed 1000 records." | "192.168.10.20"  | NULL           |

### Example 2: Limit after a filter stage

**Goal**: Restrict the number of results returned after applying specific criteria to the dataset.

**XQL code**:

```sql
dataset = sample_xql_raw
| filter is_successful = false
| limit 2
```

**Explanation**: The query first filters for events where `is_successful` is false. The `limit` stage then restricts the output to the first 2 of these filtered records.

**Output**:

| event\_id | \_time                  | event\_description             | is\_successful | duration\_seconds | simple\_json\_data                            | nested\_json\_data                                                                                      | array\_of\_json\_objects                                                | string\_tags                | numeric\_codes              | raw\_log\_data                                                       | ipv4\_address  | ipv6\_address |
| --------- | ----------------------- | ------------------------------ | -------------- | ----------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------- | --------------------------- | -------------------------------------------------------------------- | -------------- | ------------- |
| 102       | 2023-10-26 10:05:30 UTC | "File access attempt"          | false          | 0.8               | {"status": "fail", "error": "access\_denied"} | {"process": {"name": "cmd.exe", "pid": 1234}, "target": {"path": "/var/log", "permission": "rwx"\}}     | \[{"event": "file\_open", "path": "/etc/passwd"}]                       | \["filesystem", "critical"] | \[-21, 56, 13, -88, 42]     | "Process cmd.exe attempted to access /etc/passwd"                    | "10.0.0.5"     | NULL          |
| 106       | 2023-10-26 10:40:10 UTC | "Unauthorized access detected" | false          | 2.1               | {"alert\_id": "SEC-001", "severity": "high"}  | {"actor": {"type": "user", "name": "unknown"}, "target": {"resource": "db\_server", "action": "read"\}} | \[{"alert\_type": "login\_fail", "count": 5}, {"alert\_source": "IDS"}] | \["security", "attack"]     | \[-12, 24, 68, -59, 37, 80] | "Multiple failed login attempts to db\_server from external source." | "203.0.113.15" | NULL          |

### Example 3: Limit after a sort stage

**Goal**: Retrieve a specific number of top or bottom records based on a field's value.

**XQL code**:

```sql
dataset = sample_xql_raw
| sort desc duration_seconds
| limit 3
```

**Explanation**: The query sorts all records by `duration_seconds` in descending order. The `limit` stage then returns the top 3 records, effectively showing the three events with the longest duration.

**Output**:

| event\_id | \_time                  | event\_description               | is\_successful | duration\_seconds | simple\_json\_data                                | nested\_json\_data                                                                             | array\_of\_json\_objects                                                              | string\_tags                          | numeric\_codes              | raw\_log\_data                                                        | ipv4\_address  | ipv6\_address  |
| --------- | ----------------------- | -------------------------------- | -------------- | ----------------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------- | --------------------------- | --------------------------------------------------------------------- | -------------- | -------------- |
| 110       | 2023-10-26 11:00:10 UTC | "Database backup completed"      | true           | 60.0              | {"backup\_id": "DB-005", "size\_gb": 500}         | {"db": {"name": "prod\_db", "type": "SQL"}, "storage": {"location": "S3", "cost\_usd": 15\}}   | \[{"stage": "compress", "time\_s": 120}, {"stage": "upload", "time\_s": 480}]         | \["database", "backup", "successful"] | \[27, -70, 92, 11, -36, 64] | "Full backup of prod\_db to S3 completed."                            | "192.168.50.5" | NULL           |
| 108       | 2023-10-26 10:50:20 UTC | "Software update initiated"      | true           | 15.3              | {"update\_id": "SW-789", "status": "pending"}     | {"system": {"hostname": "webserver01", "os": "Linux"}, "patch": {"version": "1.2.3"\}}         | \[]                                                                                   | \["maintenance", "system"]            | \[38, -25, 73, 19, -81]     | "Patch deployment started on webserver01. Expected downtime: 15 min." | "172.20.1.100" | NULL           |
| 103       | 2023-10-26 10:15:15 UTC | "Network connection established" | true           | 10.2              | {"connection\_id": "CONN-001", "protocol": "TCP"} | {"source": {"ip": "172.16.0.1", "port": 5000}, "destination": {"ip": "1.1.1.1", "port": 443\}} | \[{"conn\_type": "outbound", "bytes": 1024}, {"conn\_type": "inbound", "bytes": 512}] | \["network", "cloud"]                 | \[90, -33, 7, 51, -62, 18]  | "Outbound connection to 1.1.1.1:443 initiated by AppX"                | NULL           | "2001:0db8::1" |

### Example 4: Limit after comp (aggregation)

**Goal**: Restrict the number of aggregated groups returned in the result set.

**XQL code**:

```sql
dataset = sample_xql_raw
| filter is_successful = true
| comp count(event_id) as successful_events by string_tags
| limit 2
```

**Explanation**: The query filters for successful events and then counts them, grouping by their `string_tags`. The `limit` stage restricts the output to just 2 of these aggregated groups.

**Output**:

| string\_tags           | successful\_events |
| ---------------------- | ------------------ |
| \["security", "login"] | 1                  |
| \["network", "cloud"]  | 1                  |

## Related articles

* **Stages**: [`comp`](comp), [`fields`](fields), [`filter`](filter), [`sort`](sort)
* **Functions**: [`count`](../functions/count_with_windowcomp_stage)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
