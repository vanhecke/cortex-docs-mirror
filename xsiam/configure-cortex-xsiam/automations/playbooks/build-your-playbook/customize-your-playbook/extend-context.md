---
description: >-
  Extend Cortex XSIAM playbook context with integration command responses, task
  data, and custom context keys.
---

# Extend context in playbooks

Integrations do not write every command response field to Cortex XSIAM playbook context. This limits context size and stores only relevant automation data.

Extend Context saves additional data from an integration command's raw response. For example, a SIEM event command might write only selected event fields to context. Extend Context lets you save fields needed for your security workflow.

Extend Context also separates outputs when a playbook runs the same command multiple times. For example, run `!ad-get-user` once for a user and again for their manager. By default, both command responses use the same context key. Extend Context writes each response to a custom playbook context key.

You can extend context in a Cortex XSIAM playbook task or from the command line. First run the command with `raw-response=true`. This helps identify data to add.

### Filter command response keys for playbook context

Use DT to select keys from a command that returns a long list of dictionaries. For example, `findIndicators` returns many indicator properties. Save only `value` and `indicator_type` to reduce context size.

For more information, see [Cortex XSOAR Transform Language (DT)](https://xsoar.pan.dev/docs/integrations/dt).

1.  Run the following command:

    ```shell
    !findIndicators size=2 query="type:IP" raw-response=true
    ```

    The response contains two dictionaries with more than 20 items each.
2.  Save only `value` and `indicator_type` to the `FoundIndicators` context key:

    ```shell
    !findIndicators size=2 query="type:IP" extend-context=`FoundIndicators=.={"value": val.value, "indicator_type": val.indicator_type}`
    ```
3.  Save only an issue name, status, and ID to the `FoundIssues` context key:

    ```shell
    !SearchIssuesV2 id=<ANY_ISSUE_ID> extend-context=`FoundIssues=Contents.data={"name": val.name, "status": val.status, "id": val.id}` ignore-outputs=true
    ```

<details>

<summary>Extend Cortex XSIAM context in a playbook task</summary>

1. Go to the **Advanced** tab of the relevant playbook task, such as a Data Collection task.
2.  In the Extend Context field, enter the name of the field in which you want the information to appear and the value you want to return. For example, using the **`!ad-get-user`** command, enter **`name="john" attributes=displayname`** to place the user's name in the **`displayName`** key.

    The following image shows the result of the **`!IPReuptation ip=20.8.1.5 raw-response=true`** command.

    [![extend-context-pb.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/cvZeKEnFBUtEoFpT3l3_Xg-5CAbsl8idaK8R43ZLhoTOw/content?v=a361064acfd013db\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/cvZeKEnFBUtEoFpT3l3_Xg-5CAbsl8idaK8R43ZLhoTOw)

    To include more than one field, separate the fields with a double colon. For example: **`attributes=displayName::manager=attributes.manager`**
3.  To output only the values for Extend context and ignore the standard output for the command, select the Ignore Outputs checkbox.

    While this will improve performance, only the values that you request in the Extend Context field are returned. You cannot use Field Mapping as there is no output to which to map the fields.

</details>

<details>

<summary>Extend Cortex XSIAM context using the CLI</summary>

1.  Run the command with `extend-context`:

    ```shell
    !<commandName> <argumentName> <value> extend-context=contextKey=JsonOutputPath
    ```

    For example, add user and manager fields with:

    ```shell
    !ad-get-user=${user.manager.username} extend-context=manager=attributes.manager::attributes=displayName
    ```
2.  Add `ignore-output=true` to return only Extend Context values:

    ```shell
    !ad-get-user=${user.manager.username} extend-context=manager=attributes.manager::attributes=displayName ignore-output=true
    ```

</details>
