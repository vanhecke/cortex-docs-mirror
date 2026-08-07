# Field replacement syntax in correlation rules

When creating correlation rules, it's possible to use predefined values for different fields in the editor, such as **Alert Name**, **Alert Description**, and **Drill-Down Query**. These predefined values follow a certain syntax and are dependent on the Cortex Query Language (XQL) query for the correlation rule that you build in the **XQL Search** and **Drill-Down Query** areas in the editor. For example, if you define the **Alert Name** to be something, such as `Alerts based on $agent_name`, the XQL query defining the correlation rule must have the `agent_name` field defined in the logic of the query; otherwise, this field won't be replaced.

<details>

<summary>Standard field replacement</summary>

Syntax

```
$<field>
```

Example:

The following text is added to the **Alert Description** field in the correlation rule editor, which uses a regular field:

`The user's registered email is: $Email`

Example Results:

If the `Email` field is a saved value containing `john.doe@example.com`, the output of the Alert Description is:

`The user's registered email is: john.doe@example.com`

Example:

The following text is added to the **Alert Description** field in the correlation rule editor, using an XDM field:

`The user's registered email is: $xdm.email.recipient`

Example Results:

If the `xdm.email.recipient` field is a saved value containing `john.doe@example.com`, the output is:

`The user's registered email is: john.doe@example.com`

Keep in mind the following:

* `<field>` identifiers must consist exclusively of alphanumeric characters (a-z, A-Z, 0-9) and underscores (`_`).
* Cortex Data Model (XDM) fields can include dot (`.`) characters.
* While `<field>` identifiers can begin with a numeric character, the fields cannot be composed solely of numeric characters. For example, `$123_data` is permissible, whereas `$456` is not.
* Text enclosed with double quotes (`"<text>"`) is treated as a literal string and will not undergo field replacement.

Example:

The following text is added to the **Alert Description** field in the correlation rule editor:

`The user's registered email is: "$Email"`

Example Results:

Since the syntax is invalid, it's ignored and the same text is displayed:

`The user's registered email is: "$Email"`

</details>

<details>

<summary>Fields with special characters</summary>

When field names contain characters that are not permitted in the standard `$<field>` syntax, such as spaces, hyphens, or special symbols, the field name must be enclosed within backticks (` `` `)

Syntax

```
$`<field>`
```

The following text is added to the **Alert Description** field in the correlation rule editor, using a field containing characters that are not permitted:

`` Report Title: $`Annual Sales Report - Q1 2025` ``

Example Results:

If the Annual Sales Report - Q1 2025 field is a saved value containing `Executive Summary`, the output is:

`Report Title: Executive Summary`

</details>
