---
description: >-
  Update Cortex XSIAM case fields with CLI commands, scripts, and playbooks to
  automate case data and investigation workflows.
---

# Update case fields

Update Cortex XSIAM case fields when an issue changes. Use CLI commands, scripts, or playbooks to automate case data updates during an investigation. For example, you can change a case name, star a case, or update its status.

You can update the following case fields through a playbook, script, or command:

* manual\_severity
* starred
* assigned\_user\_email
* status
* score
* incident\_name
* description

Use the following methods to update case fields with the CLI, a script, or a playbook.

<details>

<summary>Update case fields with the Cortex XSIAM CLI</summary>

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

<summary>Update case fields with a script</summary>

When a script runs in an issue, its data is added to the issue context data and issue fields. To update case fields, add `setParentIncidentFields` to the `demisto.executeCommand` function in a JSON file.

Example

To update the case status to `resolved`, run

```
demisto.executeCommand("setParentIncidentFields", {"status":"resolved_other"})
```

Ensure that you have the required RBAC permission to write scripts.

</details>

<details>

<summary>Update case fields with a playbook</summary>

When a playbook runs, data is added to issue context data and issue fields by default. Configure playbook tasks to also add data to case context data and case fields.

The following example explains how to add tasks to a playbook that update the case fields to star a case, and add the key starred: true to the case context data.

Add the following tasks to a new or existing playbook.

1. Create a Conditional task to check whether the parent incident fields are starred using the ${parentIncidentFields.starred} key.
2. Create a standard task using the setParentIncidentFields script to update the starred field.
3. Create a standard task to print the value to the War Room.
4. Run the playbook.\
   In the case context data, you can see the key starred: true. If running in an issue or a case, after refreshing the case, the case is now starred.

</details>
