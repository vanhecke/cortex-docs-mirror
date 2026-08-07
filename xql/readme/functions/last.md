# last

Use the last() function to retrieve the last chronologically recorded value of a specified field within a grouped set of records.

## Syntax

```sql
last (<field>)
```

## Parameters

| Name  | Type | Required | Description                                                                           |
| ----- | ---- | -------- | ------------------------------------------------------------------------------------- |
| field | any  | Yes      | The field from which to extract the last recorded value based on chronological order. |

## Returns

The last() function returns the value of the specified field from the newest (most recent) event in the evaluated group. The data type of the returned value matches the data type of the input field.

## Usage Notes

* The last() function is an aggregate function and must be used within the comp stage.
* The chronological order of the records is determined by the underlying time field (such as \_time) associated with the data events.
* If the last record contains a NULL value for the evaluated field, the function returns NULL.
* This function is frequently used in threat hunting to identify the most recent occurrence of an artifact or behavior, such as the final command executed in a session, the last known IP address for a host, or the most recent process started by a specific user.

## Examples

### Example 1: Identify the last process executed per host

**Goal**: Find the most recently recorded process name that was executed on each endpoint within the queried time frame.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = xdr_data  
| filter action_process_image_name \!= null  
| comp last(action_process_image_name) as last_process by agent_hostname  
| fields agent_hostname, last_process  
| limit 3
```

**Explanation**: The comp stage groups the events by agent\_hostname. For each unique host, the last() function evaluates the timeline of the records and returns the action\_process\_image\_name associated with the chronologically newest event in that group. The result is assigned to the last\_process alias.

**Output**:

| AGENT\_HOSTNAME | LAST\_PROCESS               |
| --------------- | --------------------------- |
| endpoint-win-01 | C:\Windows\System32\cmd.exe |
| endpoint-mac-02 | /usr/libexec/xpcproxy       |
| srv-linux-03    | /bin/bash                   |

### Example 2: Retrieve the last command line for a process

**Goal**: Identify the final command line argument used to execute a specific process across your environment before the query timeframe ended.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = xdr_data  
| filter action_process_image_name = "powershell.exe"  
| comp last(action_process_image_command_line) as final_cmd by agent_hostname  
| fields agent_hostname, final_cmd  
| limit 2
```

**Explanation**: This query filters for execution events involving powershell.exe. Using the comp stage, it groups the results by agent\_hostname and uses the last() function to extract the chronologically final command line argument executed by PowerShell on that host.

**Output**:

| AGENT\_HOSTNAME | FINAL\_CMD                                                                   |
| --------------- | ---------------------------------------------------------------------------- |
| endpoint-win-01 | powershell.exe -WindowStyle Hidden -EncodedCommand JABz...                   |
| srv-win-02      | "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -c "Get-Process" |

## Related Articles

* **Stages**: [comp](../stages/comp), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [first()](first), [earliest()](earliest), [latest()](latest)
* **Datasets**: [xdr\_data](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
