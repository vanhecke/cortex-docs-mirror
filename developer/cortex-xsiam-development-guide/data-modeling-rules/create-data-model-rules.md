---
description: >-
  Once events are ingested in the data set, create data model rules in the
  repository and then map the ingested raw events to Cortex XSIAM system fields.
---

# Create data model rules

To create a local data model rule in the Cortex XSIAM UI, see [Data modeling rules](). Follow the steps in this topic if you want to contribute the rule you created.

Once events are ingested in the data set, create data model rules in the repository and then map the ingested raw events to Cortex XSIAM system fields.

#### Create data model rules in the content repository

Create a new directory named `Packs/MyVendorMyProduct/ModelingRules/MyVendorMyProduct_1_3` inside your content pack. Create the following files within this directory:

* `MyVendorMyProduct_1_3.xif`: This file holds the XDM rule we created in the Data Model Editor in the Cortex XSIAM UI. . Copy and paste the rule directly into this file.
*   `MyVendorMyProduct_1_3.yml`: This file contains additional metadata about the data model. The file has the following structure:

    ```programlisting
    fromversion: 6.10.0  
    id: MyVendorMyProduct
    name: MyVendorMyProduct Modeling Rules
    rules: ''  
    schema: ''  
    tags: MyVendor,MyProduct
    ```
*   `MyVendorMyProduct_1_3_schema.json`: This file contains the fields that came directly from the raw response and were used in the development of the XDM rules. The file has the following structure:

    ```programlisting
    {
        "MyVendor_MyProduct_raw": {
          "field_1": {
            "type": "string|int|datetime",
            "is_array": true|false // Specify whether the field is an array/list of types.      
          },
          "field_2": {
            "type": "string|int",
            "is_array": true|false
          }
    }
    ```

    If the raw response is not a JSON-formatted string, the schema has only a `_raw_log` attribute, for example:

    ```programlisting
    {
      "MyVendor_MyProduct_raw": {
        "_raw_log": {
          "type": "string",
          "is_array": false
        }
      }
    }
    ```

#### Map event to data model rules

The next step is to map the data set of raw events to relevant data model rules. See [Data modeling rules]() in the Cortex XSIAM documentation for instructions for creating data model rules.

The data model definition begins with:

```programlisting
[MODEL: dataset="MyVendor_MyProduct_raw"]
```

Where `MyVendor` is the vendor name and `MyProduct` is the name of the vendor's product/service which we use to generate events.

Under the data model definition, write a query that maps the fields in the raw event JSON to XDM (Cortex XSIAM data model) system fields. This mapping adds the out-of-the-box enrichment capability available to all XDM system fields.

For example, the following events are sent to Cortex XSIAM and are currently in the data set `MyVendor_MyProduct_raw`:

```programlisting
[  
  {
    "id": "1234",    
    "message": "New user added 'root2'",    
    "type": "audit",    
    "op": "add",    
    "result": "success",    
    "host_info": {      
      "host": "prod-01",      
      "os": "Windows"    
    },    
    "created": "1676764803"  
   },  
   {    
    "id": "1235",    
    "message": "User 'root2' delete failed, permission denied",    
    "type": "audit",    
    "op": "delete",    
    "result": "failed",    
    "host_info": {      
      "host": "prod-01",      
      "os": "Windows"    
    },    
    "created": "1676764823"  
    }
]
```

Map each one of the JSON keys to XDM system fields. To find the relevant XDM system fields (which are prefixed with \`XDM\_CONST\`), either use the auto-completion offered by the data rules editor, or search for the fields in the [XDM field reference](https://docs-cortex.paloaltonetworks.com/r/Cortex-XSIAM/Cortex-Data-Model-Schema-Guide/Introduction).

For example, the data model rules would be defined as below:

```programlisting
[MODEL: dataset="MyVendor_MyProduct_raw"]
ALTER  
  xdm.event.id = id,  
  xdm.event.description = message,  
  xdm.event.type = type,  
  xdm.event.operation = if(
    op = "add", XDM_CONST.OPERATION_TYPE_CREATE,    
    op = "delete", XDM_CONST.OPERATION_TYPE_MODIFY,    
    op = "login", XDM_CONST.OPERATION_TYPE_LOGIN,    
    op = null, null, to_string(op)  
  ),  
  xdm.event.outcome = if(    
    result = "success", XDM_CONST.OUTCOME_SUCCESS,    
    result = "failed", XDM_CONST.OUTCOME_FAILED,    
    result = null, null, to_string(result)  
  ),  
  xdm.event.is_completed = if(result != pending),  
  xdm.source.hostname = json_extract_scalar(host_info, "$.host"),  
  xdm.source.os_family = if(    
    json_extract_scalar(host_info, "$.os") = "Windows", XDM_CONST.OS_FAMILY_WINDOWS,
    json_extract_scalar(host_info, "$.os") = null, null, to_string(json_extract_scalar(host_info, "$.os"))
  )
```

{% hint style="info" %}
### Note

* To map the `op` field to the appropriate XDM system field, in this case the `OPERATION_TYPE`, use the [XQL if](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/) function. In the example above, set the `xdm.event.operation` field to the enum `XDM_CONST.OPERATION_TYPE_CREATE` if the value of the `op` field in the raw response is `add`.
* When you use an `if` function, best practice is to have an additional argument which is used as default. You can see this additional argument at the end of the function, and it has the `field_name = null, null, to_string(field_name)` structure. You can see an example of this when defining the `op`, `result` and `os_family` fields.
* When you need to access nested fields from within the JSON, use the [`json_extract_scalar`](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/) function.
* See the [XQL Functions Reference](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/) for more information about other functions.
{% endhint %}

If at any time the query or the parsing is incorrect, the editor notifies you of the error.

After writing the rules, you can test them to verify they are mapped correctly.
