---
description: >-
  Use print to War Room, logs, and the IDE debugging resources to understand
  unexpected code behavior.
---

# Debugging

During the development phase of integrations and scripts, debugging allows you to understand what is happening behind the scenes when your code exhibits unexpected behavior. There are a few strategies that you can implement to debug code in Cortex XSIAM, described in the following sections.

#### Printing to the War Room

Seeing your statements in print is often useful when diagnosing issues. To do this, add the following to your integration/script code:

```programlisting
error_msg = "Here's your completely broken code"
demisto.log(error_msg)
```

This prints the statements in the War Room, for you to review. Remove the error messages when you are done debugging, so that they do not appear in the final code.

#### Debugging using the IDE

Sometimes debugging via printing or using the logs is not sufficient. In that case you might want to use the debugger and go through the code line by line or breakpoint by breakpoint. See [Debugging configurations for Python Apps in Visual Studio Code](https://code.visualstudio.com/docs/python/debugging).

{% hint style="info" %}
### Note

We recommend using the [Visual Studio Code extension](../readme/content-development-environments/visual-studio-code-extension) when you are developing content.
{% endhint %}

**Python Environment**

1. Prepare a Python environment with all the base dependencies. Follow the instructions in [Set up a local development environment](../readme/content-development-environments/set-up-a-local-development-environment).
2. After the Python environment is prepared, [open the integration in a virtual environment](../../readme/content-development-environments/visual-studio-code-extension#UUID-d7fd8217-1650-6334-4962-493fce34f1af_section-idm461090704812003367092331445) using the Cortex XSIAM Visual Studio Code Extension in VS Code.

**Using demistomock (the demisto object)**

The content repository includes [**demistomock.py**](https://github.com/demisto/content/blob/master/Tests/demistomock/demistomock.py) file, which usually appears as the first import in an integration or script:&#x20;

```programlisting
import demistomock as demisto
from CommonServerPython import *
from CommonServerUserPython import *
```

The **demistomock** module can be used to mock integration configuration, arguments and commands passed.

| Function             | Description                                                                 |
| -------------------- | --------------------------------------------------------------------------- |
| `demisto.params()`   | Returns the connection details inserted into the create instance in the UI. |
| `demisto.command()`  | Returns the name of the command you want to run.                            |
| `demisto.args()`     | Returns the arguments for that command.                                     |

In some cases, you might need to use other functions, and the following guidelines applies to those as well. In the `demistomock` file we can see a `params` function defined:

```programlisting
def params():
    return {}
```

This is what is returned if we run the Python file. Instead, we can fill it with the connection credentials needed to connect to our instance.

```programlisting
def params():
    return {
        "credentials":{
            "identifier": "demisto",
            "password": "password"
        },
        "server": "https://1.2.3.4/",
        "insecure": True
    }
```

and now commands such as:

```programlisting
    params: dict = demisto.params()
    username = params.get('credentials').get('identifier')  # demisto
    password = params.get('credentials').get('password')  # password
    verify_certificate = not params.get('insecure', False)
```

take their information from there.

This is called mocking demisto.

Verify that all Cortex XSIAM functions used in the functions we are testing are mocked correctly. Now we can use the debugger from the IDE or ipdb to debug the code as we would any other simple Python file.
