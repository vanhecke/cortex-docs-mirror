---
description: >-
  Store objects in the database per integration instance using the
  integrationContext command to store data between integration command runs.
---

# Integration cache

In some cases, you might need to store data between integration command runs. A common use case would be storing API tokens which have an expiration time, such as JSON Web Tokens (JTWs). Often JWTs are generated through an API call and have a validity of several minutes or hours. To avoid re-generating tokens every time a command is executed in Cortex XSIAM, you can cache them using `integrationContext` and retrieve them until they expire.

To store objects in the database per integration instance, Cortex XSIAM uses the cached object `integrationContext`.

{% hint style="info" %}
### Note

The `integrationContext` object cannot be retrieved or set in the `test-module` command.
{% endhint %}

**Implementation**

The `integrationContext` supports two methods, `getter` and `setter`. Both methods are provided by the demisto class that have wrappers in the `CommonServerPython` script. If no object is stored, the method returns an empty dictionary.

* The `get_integration_context()` method is the getter of the cached object, which returns a key-value dictionary.
* The `set_integration_context()` method is the setter of the cached object. This method takes as argument the object to store. Its keys and values must be strings. Note that this method overrides the existing object which is stored. In order to update a stored object, get it, make the requested changes, and then set it.

**Examples**

**General Usage**

```programlisting
integration_context: Dict = get_integration_context()
demisto.results(integration_context)
>>> {}
integration_context_to_set = {'token': 'TOKEN'}
set_integration_context(integration_context_to_set)
integration_context = get_integration_context()
demisto.results(integration_context['token'])
>>> "TOKEN"
integration_context_to_set = {'token': 'NEW-TOKEN'}
set_integration_context(integration_context_to_set)
integration_context = get_integration_context()
demisto.results(integration_context['token'])
>>> "NEW-TOKEN"
```

**Storing token with expiration time**

```programlisting
integration_context = get_integration_context()
token = integration_context.get('access_token')
valid_until = integration_context.get('valid_until')
time_now = int(time.time())
if token and valid_until:
    if time_now < valid_until:
        # Token is still valid - did not expire yet
        return token
# get_token() should be the implementation of retrieving the token from the API 
token = get_token()
integration_context = {
    'access_token': token,
    'valid_until': time_now + 3600  # Assuming the expiration time is 1 hour
}
set_integration_context(integration_context)
```

For more examples, see the [Microsoft Graph](https://github.com/demisto/content/blob/master/Packs/ApiModules/Scripts/MicrosoftApiModule/MicrosoftApiModule.py) and [ServiceNow](https://github.com/demisto/content/blob/master/Packs/ApiModules/Scripts/ServiceNowApiModule/ServiceNowApiModule.py) integrations.
