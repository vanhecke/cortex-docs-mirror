---
description: Add keys and values to Cortex XSIAM case context data.
---

# Add context data to a case

You can add keys and values to a case's context data to be used in playbooks or other automations. By default, context data is added to cases only. To run automations on a case, add context data to the case from its related issues.

To add context data to a case, run the `setParentIncidentContext` command in the CLI, in a script, or in a playbook task.

<details>

<summary>Use the CLI</summary>

Run the `!setParentIncidentContext` command in the issue **War Room** or the **Case War Room**.

{% hint style="info" %}
If you run the command in the issue **War Room**, the data is added to the following places:

* The case context data.
* The issue context data under the case tab.

If you run the command in the **Case War Room**, the data is added to the case context data only.
{% endhint %}

Run the command in the issue War Room

1. Open an issue and select the **War Room** tab.
2.  Run the `!setParentIncidentContext` command.

    The following example adds the key and value `hello:world` to the case and issue context data.

    ```programlisting
    !setParentIncidentContext key="hello" value="world"
    ```

Run the command in the case War Room

1. Open a case and switch to the **Detailed view**.
2. Select the **Case War Room** tab.
3.  Run the `!setParentIncidentContext` command.

    The following example adds the key and value `hello:world` to the case context data.

    ```programlisting
    !setParentIncidentContext key="hello" value="world"
    ```

</details>

<details>

<summary>Use a script</summary>

In any script that runs in an issue, the data is written to the issue context data. If you want to add the data to the case context from your script, run the `setParentIncidentContext` using the `demisto.executeCommand` key, as follows:

`demisto.executeCommand("setParentIncidentContext", {"key":"<key>", "value":"<value>"})`

The following example creates a new key name `AuditID` with a `90210` value to your script.

```programlisting
demisto.executeCommand("setParentIncidentContext", {"key":"AuditID", "value":"90210"})
```

</details>

<details>

<summary>Use a playbook</summary>

When a playbook runs, the playbook data is written to the issue context data. To write the data to the parent case context data, use the `setParentIncidentContext` script in a standard task.

The following example adds the TicketID to the case context. To see a full use case that includes this standard task, see [Use context data in a playbook](#UUID-050987be-fc55-bed7-3671-8170a9a2e58c).

![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-65b0c21bb12e897c8991a96766fafd756a9d646b%2F7f674a2d336e611aa5e5be825eb39356aa17a576613e32eea3160163d9fdbd62.png?alt=media)

</details>
