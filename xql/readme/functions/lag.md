# lag

Use the lag() function to access data from a preceding row in the same result set, enabling comparisons between the current row and a previous one.

## Syntax

lag(\<field>, \<offset>, \<default\_value>)

## Parameters

| Name           | Type    | Required | Description                                                                                                                                      |
| -------------- | ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| field          | any     | Yes      | The field from which to extract the value.                                                                                                       |
| offset         | integer | No       | The number of rows back from the current row from which to obtain a value. The default is 1.                                                     |
| default\_value | any     | No       | The value to return if the offset points to a row that does not exist (for example, before the first row of the partition). The default is NULL. |

## Returns

The lag() function returns the value of the specified field from the row that is the specified number of rows before the current row. The data type matches the data type of the input field.

## Usage Notes

* The lag() function is an analytic function and must be used within the windowcomp stage.
* The chronological or logical order of the records is determined by the order by clause within the over() partition statement.
* This function is frequently used to calculate differences between consecutive events, such as the time elapsed between logins or the change in file size between versions.

## Examples

### Example 1: Identify consecutive processes

**Goal**: Check the previous process name that was executed.

**XQL Code**:

```sql
dataset \= xdr_data
| filter action_process_image_name != null
| windowcomp lag(action_process_image_name) as previous_process over(partition by agent_hostname order by _time asc)
| fields agent_hostname, action_process_image_name, previous_process, _time
| sort asc agent_hostname , _time
```

**Explanation**: The windowcomp partition operates within the parameters defined in the over() partition statement. The query organizes the data to evaluate by agent\_hostname according to the ascending chronological order of its creation time. The results returned in the new field previous\_process provide the process image name of the previous event for each agent hostname. Because this calculation utilizes the windowcomp stage, all lines of the dataset are returned along with this new field value.

**Output**:

| AGENT\_HOSTNAME | ACTION\_PROCESS\_IMAGE\_NAME | PREVIOUS\_PROCESS | \_TIME                 |
| --------------- | ---------------------------- | ----------------- | ---------------------- |
| mac-agent-1     | test-process-1               | null              | Mar 26th 2026 09:26:07 |
| mac-agent-1     | test-process-2               | test-process-1    | Mar 26th 2026 09:26:08 |
| mac-agent-1     | test-process-3               | test-process-2    | Mar 26th 2026 09:26:09 |

## Related Articles

* **Stages**: [windowcomp](../stages/windowcomp), [filter](../stages/filter), [fields](../stages/fields), [sort](../stages/sort)
* **Functions**: lead(), [first\_value()](first_value), [last\_value()](last_value)
* **Datasets**: [xdr\_data](https://docs-cortex.paloaltonetworks.com/r/Cortex-XQL-Schema-Reference-Guide/Introduction)
