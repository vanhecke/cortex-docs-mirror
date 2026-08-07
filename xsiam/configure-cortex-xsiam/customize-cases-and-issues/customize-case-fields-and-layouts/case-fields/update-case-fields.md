# Update case fields

Sometimes you need to update case fields based on a change in an issue. For example, after starting an investigation an analyst might want to change the name of a case, star a case, or change the status of a case.

You can update the following case fields through a playbook, script, or command:

* manual\_severity
* starred
* assigned\_user\_email
* status
* score
* incident\_name
* description

The following sections explain how to update case fields by running a command in the CLI, and running a script, and running a playbook.

<details>

<summary>Use the CLI</summary>

Run the `!setParentIncidentFields` command in the issue or case War Room.

When you start typing the CLI provides the available options. If you select an enum field the CLI provides the available values.

Examples

*   To change the name of the case to `Malware`, run

    ```
    !setParentIncidentFields incident_name=Malware
    ```
*   To change the name of the case to `Malware` and star the case, run

    ```
    !setParentIncidentFields incident_name=Malware starred=true
    ```

</details>

<details>

<summary>Use a script</summary>

When a script runs in an issue, the data from the script is added to the issue context data and the issue fields. If you want to update case fields, in a Json file, add the `setParentIncidentFields` to the `demisto.executeCommand` function.

Example

To update the case status to `resolved`, run

```
demisto.executeCommand("setParentIncidentFields", {"status":"resolved_other"})
```

Ensure that you have the required RBAC permission to write scripts.

</details>

<details>

<summary>Use a playbook</summary>

When running a playbook, by default the data is added to the issue context data and issue fields. You can additionally add this data to case context data and case fields by configuring tasks in a playbook.

The following example explains how to add tasks to a playbook that update the case fields to star a case, and add the key starred: true to the case context data.

Add the following tasks to a new or existing playbook.

1. Create a Conditional task to check whether the parent incident fields are starred using the ${parentIncidentFields.starred} key.
2. Create a standard task using the setParentIncidentFields script to update the starred field.
3. Create a standard task to print the value to the War Room.
4. Run the playbook.\
   In the case context data, you can see the key starred: true. If running in an issue or a case, after refreshing the case, the case is now starred.

</details>
