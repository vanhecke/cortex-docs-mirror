# regexcapture

Use the `regexcapture()` function to extract from a string substrings that match specified named regular expression groups and return them as a JSON object.

## Syntax

```sql
regexcapture (<field>, "<pattern>")
```

## Parameters

| Name      | Type   | Required | Description                                                                                                  |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------ |
| `field`   | string | Yes      | The string field (typically `_raw_log`) or literal to apply the regex to.                                    |
| `pattern` | string | Yes      | The regular expression string, enclosed in double quotes, containing named capture groups (`(?P<name>...)`). |

## Returns

The `regexcapture()` function returns a JSON object where the keys correspond to the named capture groups defined in the regex pattern, and the values are the extracted substrings.

## Usage notes

* The `regexcapture()` function is **only supported in the XQL syntax for parsing rules**. The function cannot be used directly in an `alter` or `filter` stage within an interactive XQL query submitted via the Query Builder.
* XQL utilizes the RE2 regular expression implementation.
* For case-insensitive matching, you can include `(?i)` at the beginning of your regular expression pattern. This syntax must be added only once at the beginning of the inline regular expression.
* Unlike the `regextract()` function, which typically supports only one capturing group in queries, `regexcapture()` is designed for capturing **multiple named groups** within a single pattern.
* The function is ideal for scenarios where the exact regex pattern might vary across logs, offering flexible extraction into structured JSON.

## Examples

### Example 1: Extracting user and IP address from a login log

**Goal**: Extract the username and source IP address from a raw log using named capture groups.

**XQL code**:

```sql
// This example demonstrates how regexcapture() is defined in a Parsing Rule
// and simulates the output using standard XQL functions for display purposes.

// Parsing Rule Syntax:
// alter captured_details = regexcapture(_raw_log, "User (?P<username>\w+) logged in from (?P<source_ip>\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})");

// Simulated Query to visualize the result:
config timeframe = 1d
| dataset = sample_xql_raw
| alter log_entry = raw_log_data
| alter extracted_info =
    if(event_id = 101,
       object_create(
           "username", "Alice",
           "source_ip", "192.168.1.10"
       ),
       NULL
    )
| fields event_id, log_entry, extracted_info
| limit 1
```

**Explanation**: A conceptual Parsing Rule would apply the regex pattern to the raw log. The named groups `username` and `source_ip` would capture "Alice" and "192.168.1.10" respectively, forming the JSON object `{"username": "Alice", "source_ip": "192.168.1.10"}` in the `extracted_info` field.

**Output**:

| EVENT\_ID | LOG\_ENTRY                               | EXTRACTED\_INFO                                     |
| --------- | ---------------------------------------- | --------------------------------------------------- |
| 101       | "User Alice logged in from 192.168.1.10" | {"username": "Alice", "source\_ip": "192.168.1.10"} |

### Example 2: Extracting process name and file path from an access log

**Goal**: Extract a process name and a file path from a system log entry.

**XQL code**:

```sql
// This example demonstrates how regexcapture() is defined in a Parsing Rule
// and simulates the output using standard XQL functions for display purposes.

// Parsing Rule Syntax:
// alter captured_process_data = regexcapture(_raw_log, "Process (?P<process_name>[a-zA-Z0-9.]+?) attempted to access (?P<file_path>.*)");

// Simulated Query to visualize the result:
config timeframe = 1d
| dataset = sample_xql_raw
| alter log_entry = raw_log_data
| alter extracted_info =
    if(event_id = 102,
       object_create(
           "process_name", "cmd.exe",
           "file_path", "/etc/passwd"
       ),
       NULL
    )
| fields event_id, log_entry, extracted_info
| limit 1
```

**Explanation**: The conceptual Parsing Rule extracts "cmd.exe" into `process_name` and "/etc/passwd" into `file_path`, creating the corresponding JSON object.

**Output**:

| EVENT\_ID | LOG\_ENTRY                                        | EXTRACTED\_INFO                                           |
| --------- | ------------------------------------------------- | --------------------------------------------------------- |
| 102       | "Process cmd.exe attempted to access /etc/passwd" | {"process\_name": "cmd.exe", "file\_path": "/etc/passwd"} |

### Example 3: Extracting destination IP address, port, and application ID (with case-insensitive matching)

**Goal**: Extract network details and an application ID from a network connection log using case-insensitive matching.

**XQL code**:

```sql
// This example demonstrates how regexcapture() is defined in a Parsing Rule
// and simulates the output using standard XQL functions for display purposes.

// Parsing Rule Syntax:
// alter captured_network_details = regexcapture(_raw_log, "(?i)connection to (?P<dest_ip>\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}):(?P<port>\d+) initiated by (?P<app_id>[^ ]+)");

// Simulated Query to visualize the result:
config timeframe = 1d
| dataset = sample_xql_raw
| alter log_entry = raw_log_data
| alter extracted_info =
    if(event_id = 103,
       object_create(
           "dest_ip", "1.1.1.1",
           "port", "443",
           "app_id", "AppX"
       ),
       NULL
    )
| fields event_id, log_entry, extracted_info
| limit 1
```

**Explanation**: The conceptual Parsing Rule uses `(?i)` for case-insensitivity and extracts the destination IP, port, and application ID, demonstrating the capability to parse varied log structures into structured JSON objects.

**Output**:

| EVENT\_ID | LOG\_ENTRY                                             | EXTRACTED\_INFO                                           |
| --------- | ------------------------------------------------------ | --------------------------------------------------------- |
| 103       | "Outbound connection to 1.1.1.1:443 initiated by AppX" | {"dest\_ip": "1.1.1.1", "port": "443", "app\_id": "AppX"} |

## Related articles

* **Stages**: [`alter`](../stages/alter)
* **Functions**: [`regextract`](regextract), [`json_extract`](json_extract), [`object_create`](object_create)
* **Datasets**: [`xdr_data`](https://www.google.com/search?q=%5Bhttps://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction%5D\(https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction\))
