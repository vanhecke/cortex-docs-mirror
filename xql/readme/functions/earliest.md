# earliest

Use the earliest() function to retrieve the chronologically oldest value of a specified field within a grouped set of records.

## Syntax

earliest(\<field>)

## Parameters

| Name  | Type | Required | Description                                                                      |
| ----- | ---- | -------- | -------------------------------------------------------------------------------- |
| field | any  | Yes      | The field from which to extract the earliest value based on chronological order. |

## Returns

The earliest() function returns the value of the specified field from the oldest event in the evaluated group. The data type of the returned value matches the data type of the input field.

## Usage Notes

* The earliest() function is an aggregate function and must be used within the comp stage.
* The chronological order of the records is determined by the underlying time field (such as \_time) associated with the data events.
* If the earliest record contains a NULL value for the evaluated field, the function will return NULL.
* This function pairs frequently with the comp stage's by clause to find the first occurrence of an activity (like a process execution or login) per user or host.

## Examples

### Example 1: Identify the First Process Executed per Host

**Goal**: Find the earliest recorded process name that was executed on each endpoint within the queried time frame.

**XQL Code**:

```sql
config timeframe \= 1d  
| dataset \= xdr_data  
| filter action_process_image_name \!= null  
| comp earliest(action_process_image_name) as first_process by agent_hostname  
| fields agent_hostname, first_process  
| limit 3
```

**Explanation**: You use the comp stage to group the events by agent\_hostname. For each unique host, the earliest() function evaluates the timeline of the records and returns the action\_process\_image\_name associated with the chronologically oldest event in that group. The result is assigned to the first\_process alias.

**Output**:

| AGENT\_HOSTNAME | FIRST\_PROCESS               |
| --------------- | ---------------------------- |
| endpoint-win-01 | C:\Windows\System32\smss.exe |
| endpoint-mac-02 | /sbin/launchd                |
| srv-linux-03    | /usr/lib/systemd/systemd     |

## Related Articles

* **Stages**: [comp](../stages/comp), [filter](../stages/filter), [fields](../stages/fields), [limit](../stages/limit)
* **Functions**: [latest()](latest), [first()](first), [last()](last)
* **Datasets**: [xdr\_data](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
