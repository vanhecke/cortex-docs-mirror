---
description: Cortex XSIAM steps for testing data model rules.
---

# Test Data Model Rules

After writing data model rules, test them to ensure the rules work as expected.

There are two ways to test the modeling rules:

* Use an [XQL query](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/detect-investigate-and-respond-to-threats/investigation-and-response/build-xql-queries/how-to-build-xql-queries/create-xql-query) in the Cortex XSIAM UI.
* Create a data model test configuration and execute the test using `demisto-sdk`.

### **Example JSON and data modeling rules**

Use the sample JSON and data model rules as described in [Create data model rules]().

The JSON file represents the ingested events:

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

The following are sample data model rules:

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

**Test data model rules using the Cortex XSIAM UI**

After creating the XDM rules and ensuring no errors were raised, construct a new XQL query with the fields mapped in the data model. Using the data model above, the query looks like this:

`datamodel dataset in("MyVendor_MyProduct_raw") |`

`FIELDS`

`xdm.event.id,`

`xdm.event.description,`

`xdm.event.type,`

`xdm.event.outcome,`

`xdm.event.operation,`

`xdm.event.is_completed,`

`xdm.source.hostname,`

`xdm.source.os_family`

{% hint style="info" %}
### Tip

Only select fields are mapped in the data model to make it easier to review the actual and expected results.
{% endhint %}
