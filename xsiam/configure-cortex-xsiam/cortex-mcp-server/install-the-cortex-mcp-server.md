---
description: >-
  Install and configure the Cortex MCP Server with Docker or Poetry to
  investigate and manage Cortex XSIAM cases from an MCP client.
---

# Install the Cortex MCP server

With the Cortex MCP Server, you can use natural language in your MCP client to investigate and manage cases and issues. The MCP Server can be run within a Docker container or a Poetry virtual environment.

This documentation contains instructions for configuring and using the Cortex MCP server. More detailed setup instructions are provided in the README file included in the download.

These instructions use Claude Desktop, but you can use any client that supports MCP.

{% hint style="info" %}
#### **Prerequisite**

If you plan to run the Cortex MCP server in a Poetry virtual environment, you must have Python 3.13 or higher.

If you plan to run the Cortex MCP server in a Docker container, you must have Docker installed.
{% endhint %}

{% stepper %}
{% step %}
### **Download the Cortex MCP server**

1. Go to Settings → Configurations → Integrations → Cortex MCP Server.
2. Download MCP File
3. (Optional) Download the checksum file and run a command such as `shasum` (Linux/macOS) or `certutil` (Windows) to verify the integrity and the file authenticity. For example: `shasum -a 256 -c cortex-checksum.zip.sha256`.
4. Extract the .zip file.
5. From the Cortex MCP Server page in Cortex XSIAM, click the link to open the page to create a new API key.
{% endstep %}

{% step %}
### **Create an API key**

{% hint style="info" %}
The MCP Server uses public APIs to communicate and is limited by the license quotas available in your tenant. This is particularly relevant when running XQL queries. For more information on running XQL query APIs, see [Run XQL query APIs](https://app.gitbook.com/s/1ZrobAtcwfCDWAJAWeuj/cortex-platform/run-xql-query-apis).
{% endhint %}

1.  Either click the link from the Cortex MCP Server page or navigate to Settings → Configurations → Integrations → API Keys → New Key.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you click the link from the Cortex MCP Server page, the Standard security level is selected, the Viewer role is prepopulated, and an expiration date is enabled. If you navigate directly to the API Keys page, configure the API key as described below.</p></div>
2. In the Role tab, perform the following:
   1. Under Security Level, select Standard.
   2.  Under Role, select the desired access level for this key. You can select from predefined roles or custom roles. Roles are available according to what was defined in either the Cortex Gateway or the tenant's Access Management. You can view the configuration of the role selected by expanding the sections under Components.

       <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>It is critical to avoid assigning excessive permissions when creating an API key for the Cortex MCP Server. Since the key has both read and write capabilities, overly broad permissions can lead to unintended actions and potentially compromise your environment. Ensure the key follows the principle of least privilege and is granted only the minimum required access.</p></div>
   3. (Optional) Under Comment, provide a comment that describes the purpose of the API key.
   4. (Optional) If you want to define a time limit on the API key authentication, select Enable Expiration Date, and select the expiration date and time. You can track the expiration date of each API key in the API Keys page. In addition, an API Key Expiration notification appears in the Notification Center one week and one day before the defined expiration date.
3. (Optional) If Scope-Based Access Control (SBAC) is enabled for the tenant, click Scope, and under Scope Definition, select the scope areas that you want to limit the user role to access for this API.
4. Click Generate to generate the API key.
5.  Copy the generated API key and click Done.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>To configure the Cortex MCP Server, you need the Cortex API URL, Cortex API key, and Cortex API key ID. You will not be able to view the API key again after you complete this step. Ensure that you copy the API key before closing the notification.</p></div>
{% endstep %}

{% step %}
### **Install and run the Cortex MCP Server**

{% hint style="info" %}
By default, stdio (standard input/output) is used. You can also configure Streamable HTTP to send requests directly to the tenant instead of through the MCP client. Streamable HTTP can be useful for testing in the browser without an MCP client and to bypass limits that may be in place for your MCP client. For Docker, you can include the Streamable HTTP variables in the .env file. You can also include it as a flag when you start the server in the Python virtual environment.
{% endhint %}

In the extracted files, follow the detailed instructions in the README.md file located in the top directory. Instructions are provided for both Docker and Poetry and include the following:

Docker

1.  Create an .env file with the environment variables.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>When using Docker, we recommend using an .env file to set the Cortex API credentials as environment variables. While the credentials can be provided in the MCP client configuration settings, the .env file provides safer handling of API credentials and makes your configuration easily reproducible.</p></div>
2. Build and run the Docker container.
3. Run the Docker container: `docker run --env-file .env -it cortex-mcp`.

Poetry

1. Install Poetry.
2. Create and activate a virtual environment.
3. Install project dependencies.
4. Provide the required variables in the Python runtime environment.
5.  Start the server: `python src/main.py`.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>When using the Poetry virtual environment, you can also start the server using the CLI command <code>python src/cli.py start [OPTIONS</code>, where [OPTIONS] includes the API key id, API key, the Cortex PAPI server URL, and the log level.</p></div>
{% endstep %}
{% endstepper %}

### **Use Cortex MCP Server CLI commands**

From the CLI, you can run three commands.

* `start`: Start the Cortex MCP server. Relevant only for the Poetry virtual environment.
* `update`: Any new or updated components provided by Cortex are automatically downloaded into the builtin\_components folder. During each update, the folder is fully replaced, and all existing contents are recreated. Do not add custom tools to this directory, as it is managed entirely by Cortex and is overwritten at every update.
* `version`: Displays the current version of the Cortex MCP Server.

Additional information about the CLI is available in the README file located in the `src` directory.
