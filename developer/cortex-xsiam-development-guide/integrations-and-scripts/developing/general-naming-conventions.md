---
description: Naming conventions for integrations, commands, arguments, and outputs.
---

# General naming conventions

When naming integrations, commands, arguments and outputs, use the following conventions:

*   Integration parameters

    Use brief and clear names with `snake_case`. Example: `min_severity`
*   Command names

    Use kebab-case with the structure `!vendor-action-object`. Example: `!helloworld-get-alert`
*   Command arguments

    Use brief and clear names with `snake_case`. Example: `alert_id`.
*   Command outputs

    Use `PascalCase` with the structure Vendor.Object.data for the Vendor and Object block. Example: `HelloWorld.Alert.owner.name`

    After the Vendor and Object blocks, use the same format as your product's API, but do not include any spaces or dots in the key names, as dots are interpreted as object separators. For example, Cortex XSIAM correctly parses:

    ````programlisting
    ```json
    {
      "HelloWorld": {
        "Alert": {
          "owner": {
              "name": "Francesco",
              "email": "francesco@cortex.local"
          }
        }
      }
    }
    ```
    as:
    ```
    HelloWorld.Alert.owner.name: "Francesco"
    HelloWorld.Alert.owner.email: "francesco@cortex.local"
    ```
    ````

    Cortex XSIAM does NOT correctly parse:

    ````programlisting
    ```json
        {
      "HelloWorld": {
        "Alert": {
          "owner.name": "Francesco",
          "owner.email": "francesco@cortexl.local"
        }
      }
    }
    ```
    ````
