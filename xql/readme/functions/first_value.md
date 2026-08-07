# first\_value

Use the first\_value() function to retrieve the first value of a specified field within an ordered partition of records, typically used for baseline comparisons across a sequence of events.

## Syntax

first\_value(\<field>)

## Parameters

| Name  | Type | Required | Description                                                                                      |
| ----- | ---- | -------- | ------------------------------------------------------------------------------------------------ |
| field | any  | Yes      | The field from which to extract the first recorded value based on the window's defined ordering. |

## Returns

The first\_value() function returns the value of the specified field from the first row of the evaluated window frame. The data type of the returned value matches the data type of the input field.

## Usage Notes

* The first\_value() function is a window function and must be used strictly within the windowcomp stage.
* The chronological or logical order of the records is determined by the order by clause within the over() partition statement.
* Unlike the first() aggregate function used in the comp stage, first\_value() appends the retrieved baseline value to _every_ row in the partition without collapsing the dataset, enabling row-by-row comparative analysis.
* If the evaluated field for the first row in the window is NULL, the function will return NULL for the records in that window frame.

## Examples

### Example 1: Establish an Initial Process Baseline per Host\*\*

**Goal**: Identify the first recorded process name executed on each endpoint and append this baseline value alongside all subsequent process executions to spot deviations.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = xdr_data  
| filter action_process_image_name != null  
| windowcomp first_value(action_process_image_name) as initial_process over(partition by agent_hostname order by _time asc)  
| fields _time, agent_hostname, action_process_image_name, initial_process  
| limit 3
```

**Explanation**: You use the windowcomp stage to partition the events by agent\_hostname and order them chronologically using \_time asc. The first\_value() function evaluates this ordered window and captures the first action\_process\_image\_name encountered in each partition. This value is assigned to the initial\_process alias and appended to every row for that host, allowing you to easily compare the current process (action\_process\_image\_name) against the first process (initial\_process).

**Output**:

| \_TIME                  | AGENT\_HOSTNAME | ACTION\_PROCESS\_IMAGE\_NAME       | INITIAL\_PROCESS             |
| ----------------------- | --------------- | ---------------------------------- | ---------------------------- |
| 2023-10-26 10:00:00 UTC | endpoint-win-01 | C:\Windows\System32\smss.exe       | C:\Windows\System32\smss.exe |
| 2023-10-26 10:05:30 UTC | endpoint-win-01 | C:\Windows\System32\cmd.exe        | C:\Windows\System32\smss.exe |
| 2023-10-26 10:20:00 UTC | endpoint-win-01 | C:\Windows\System32\powershell.exe | C:\Windows\System32\smss.exe |

### Example 2: Return the first value of a field

**Goal**: Extract the original remote port in a network connection.

**XQL Code**:

```sql
dataset = xdr_data
| filter event_type = ENUM.NETWORK
| filter action_remote_port != null  
| windowcomp first_value(action_remote_port) as first_remote_port over(partition by agent_hostname order by _time asc)
| fields agent_hostname, action_remote_port, first_remote_port, _time
| sort asc agent_hostname , _time
```

**Explanation**: The windowcomp partition operates within the parameters defined in the over() partition statement. The query organizes the data to evaluate by agent\_hostname according to the ascending chronological order of its creation time. The results returned in the new field first\_remote\_port provide the remote port value of the earliest creation time event for each agent hostname. Because this calculation utilizes the windowcomp stage, all lines of the dataset are returned along with this new field value.

**Output**:

| AGENT\_HOSTNAME | ACTION\_REMOTE\_PORT | FIRST\_REMOTE\_PORT | \_TIME                 |
| --------------- | -------------------- | ------------------- | ---------------------- |
| mac-agent-1     | 443                  | 443                 | Mar 26th 2026 09:26:07 |
| mac-agent-1     | 443                  | 443                 | Mar 26th 2026 09:26:08 |
| mac-agent-1     | 80                   | 443                 | Mar 26th 2026 09:26:09 |

## Related Articles

* **Stages**: [windowcomp](../stages/windowcomp), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [last\_value()](last_value), [first()](first), [lag()](lag)
* **Datasets**: [xdr\_data](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
