---
description: Create a sample integration for Cortex XSIAM.
---

# Create a sample integration

You can develop integrations using the built-in IDE in the Cortex XSIAM UI or using Visual Studio Code with the Visual Studio extension.

In this example, we use the IDE in the Cortex XSIAM UI, which includes access to Script Helper (a library of many common server functions within Cortex XSIAM) as well as a graphical user interface for editing integration settings, commands, and arguments.

#### CommonServerPython and CommonServerUserPython

The [CommonServerPython (CSP)](https://xsoar.pan.dev/docs/reference/api/common-server-python) and [CommonServerUserPython (CSUP)](https://xsoar.pan.dev/docs/reference/scripts/common-server-user-python) scripts are implicitly imported at the beginning of every Python script in Cortex XSIAM. CSP is imported first, enabling you to create your own common methods in CSUP to use across scripts and integrations.

{% hint style="info" %}
### Note

CSP and CSUP can’t be attached to integrations you create, so any changes you implement are not available for other users.
{% endhint %}

#### Script Helper

In many cases, there is already an existing script for common server functions. With the Script Helper, you can find tools for example to format a table, manipulate data, and post to the War Room. If a function you want to create seems like it could be used in many different scripts, there’s a good chance it already exists in Script Helper. If you do create a new function that you believe would be useful across many scripts, we encourage you to contribute that function to [CommonServerPython](https://github.com/demisto/content/blob/master/Packs/Base/Scripts/CommonServerPython/CommonServerPython.py) scripts.

Follow these steps to create an integration from the IDE in the Cortex XSIAM UI.

1.  In Cortex XSIAM, navigate to **Settings** → **Data Collection** → **Automation & Feed Integrations** and click **BYOI** in the top right corner.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you don’t see this button, it means you don’t have the correct permissions required for creating new integrations. Contact your admin for assistance.</p></div>
2. [Define integration settings](create-a-sample-integration/define-sample-integration-settings).
3. [Write the integration code](create-a-sample-integration/write-integration-code).
4. [Test the integration](create-a-sample-integration/test-the-integration).
