# first

Use the first() function to retrieve the first chronologically recorded value of a specified field within a grouped set of records.

## Syntax

first(\<field>)

## Parameters

| Name  | Type | Required | Description                                                                            |
| ----- | ---- | -------- | -------------------------------------------------------------------------------------- |
| field | any  | Yes      | The field from which to extract the first recorded value based on chronological order. |

## Returns

The first() function returns the value of the specified field from the oldest event in the evaluated group. The data type of the returned value matches the data type of the input field.

## Usage Notes

* The first() function is an aggregate function and must be used within the comp stage.
* The chronological order of the records is determined by the underlying time field (such as \_time) associated with the data events.
* If the first record contains a NULL value for the evaluated field, the function will return NULL.
* This function is frequently used in threat hunting to identify the initial occurrence of an artifact or behavior, such as the first command executed in a session or the initial process started by a specific user.

## Examples

### Example 1: Identify the First Process Executed per Host

**Goal**: Find the first recorded process name that was executed on each endpoint within the queried time frame.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = xdr_data  
| filter action_process_image_name != null  
| comp first(action_process_image_name) as first_process by agent_hostname  
| fields agent_hostname, first_process  
| limit 3
```

**Explanation**: You use the comp stage to group the events by agent\_hostname. For each unique host, the first() function evaluates the timeline of the records and returns the action\_process\_image\_name associated with the chronologically oldest event in that group. The result is assigned to the first\_process alias.

**Output**:

| AGENT\_HOSTNAME | FIRST\_PROCESS               |
| --------------- | ---------------------------- |
| endpoint-win-01 | C:\Windows\System32\smss.exe |
| endpoint-mac-02 | /sbin/launchd                |
| srv-linux-03    | /usr/lib/systemd/systemd     |

### Example 2: Retrieve the First Command Line for a Process

**Goal**: Identify the first command line argument used to execute a specific process across your environment.

**XQL Code**:

```sql
config timeframe = 1d  
| dataset = xdr_data  
| filter action_process_image_name = "powershell.exe"  
| comp first(action_process_image_command_line) as initial_cmd by agent_hostname  
| fields agent_hostname, initial_cmd  
| limit 2
```

**Explanation**: This query filters for execution events involving powershell.exe. Using the comp stage, it groups the results by agent\_hostname and uses the first() function to extract the chronologically first command line argument executed by PowerShell on that host.

**Output**:

| AGENT\_HOSTNAME | INITIAL\_CMD                                                           |
| --------------- | ---------------------------------------------------------------------- |
| endpoint-win-01 | powershell.exe -ExecutionPolicy Bypass -File C:\scripts\setup.ps1      |
| srv-win-02      | "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile |

## **Related Articles**

* **Stages**: [comp](../stages/comp), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [earliest()](earliest), [last()](last), [latest()](latest)
* **Datasets**: [xdr\_data](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
