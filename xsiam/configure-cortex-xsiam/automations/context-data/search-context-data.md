---
description: Search and expand values in context data.
---

# Search context data

You can use Query to search within the context data JSON for specific items and expand nested keys. Open the context data panel for an issue or case, as explained in [Issue context data](issue-context-data) or [Case context data](case-context-data), and type in the **Search** field.

Example context:

```programlisting
{
  "HelloWorld": {
    "Alerts": [
      {
        "name": "Example 1",
        "alert_status": "ACTIVE"
      },
      {
        "name": "Example 2",
        "alert_status": "CLOSED"
      },
      {
        "name": "Example 3",
        "alert_status": "ACTIVE"
      }
    ]
  }
}
```

Search examples:

* `${c}` finds the value of the object c.
* `${HelloWorld.Alert(val.name == 'Example 1')}` shows the full object for the alert named "Example 1", as stored in the context data.
* `${HelloWorld.Alert(val.alert_status === "ACTIVE")}` shows the full object for all alerts in context with status "ACTIVE".
* `${HelloWorld.Alert(val.alert_status == 'ACTIVE').name}` fetches the HelloWorld.Alert.name of all alerts in context with status "ACTIVE".
