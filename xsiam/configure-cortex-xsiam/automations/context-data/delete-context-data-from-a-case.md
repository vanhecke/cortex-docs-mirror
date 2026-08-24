---
description: Delete all or selected Cortex XSIAM context data from a case.
---

# Delete context data from a case

Run the `!deleteParentIncidentContext` command to delete all context data or a specific key in the **Case War Room** or issue **War Room**.

Use the issue War Room

1. Open an issue and select the **War Room** tab.
2. Run the `!deleteParentIncidentContext` command.

Use the case War Room

1. Open a case and switch to the **Detailed View**.
2. Select the **Case War Room** tab.
3. Run the `!deleteParentIncidentContext` command.

The following example deletes the key and value `hello:world` from the case or issue context.

```programlisting
!deleteParentIncidentContext key="hello" value="world"
```
