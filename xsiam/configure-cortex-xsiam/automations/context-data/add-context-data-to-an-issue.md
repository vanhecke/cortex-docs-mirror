---
description: Add keys and values to Cortex XSIAM issue context data.
---

# Add context data to an issue

You can add keys and values to an issue's context data to be used in playbooks or other automations.

To add context data to an issue, run the `Set` command in CLI, in a script, or in a playbook task. The Set command enables you to set a value under a specific key. For more information about the Set command, see [Set](https://xsoar.pan.dev/docs/reference/scripts/set).

<details>

<summary>Use the CLI</summary>

Run the `!Set` command in the issue **War Room**.

1. Open an issue and select the **War Room** tab.
2.  Run the `!Set` command.

    **Example**

    The following example adds the key and value `hello:world` to the issue context data.

    ```programlisting
    !set key="hello" value="world"
    ```

</details>

<details>

<summary>Use a script</summary>

In the JSON file, add `Set` to the `demisto.executeCommand` key.

Example

The following example adds the key and value `hello:world` to the issue context data.

```programlisting
demisto.executeCommand("Set", {"key":"hello", "value":"world"})
```

</details>

<details>

<summary>Use a playbook</summary>

Use the `Set` script in a standard task.

Example

An issue's context data contains the following values:

```programlisting
{   
   "Account":
    {
      "firstName": "Bob",
      "lastName": "Jones",
    }
}
```

For an automation, you need to use the full name value. You can use the `Set` script to add an new `fullName` value to the JSON:

![addcontextdata.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-82986a33c7b8e46910c5963c09d5811b6be8f566%2F779c2f7fdb309c1925c0d54779d76838e7a38f47c110e44cf7d2506dfebdd26c.png?alt=media)

Result:

```programlisting
{   
   "Account":
    {
      "firstName": "Bob",
      "fullName": "Bob Jones"
      "lastName": "Jones",
    }
}
```

</details>
