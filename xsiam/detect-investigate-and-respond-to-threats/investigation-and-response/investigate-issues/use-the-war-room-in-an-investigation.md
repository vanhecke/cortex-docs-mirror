# Use the War Room in an investigation

## Use the War Room in an investigation

The War Room contains an audit trail of all automatic or manual actions that take place in a case or issue. A War Room is where you can review and interact with your case or issue. Cortex XSIAM provides machine learning insights to suggest the most effective analysts and command-sets. Each case and issue has a unique War Room.

![war-room-overview.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f92a851dc704e7a4b7979bc6f452bb88dbee9848%2Fae739b32b1d0c475e000690359637f178f3a7c9b3a08e61a2f6843c9307a21ca.png?alt=media)

### Investigate in the War Room

Within Cortex XSIAM, real-time investigation is facilitated through the War Room, which is powered by ChatOps. In the War Room you can take the following actions:

* Run real-time security actions through the CLI, without switching consoles
* Run security playbooks, scripts, and commands
* Collaborate and execute remote actions across integrated products
* Capture case context from different sources.
* Document all actions in one source.
* Communicate with others for joint investigations.

{% hint style="info" %}
### Note

The case War Room is usually used for communication capabilities, but unlike the issue War Room, it does not include playbook specific entries. The case War Room enables you to investigate an entire case, not just an issue.
{% endhint %}

### Use the Playground

Every case has a War Room, but every user has access, subject to permissions, to a private War Room called the Playground.

The Playground is a non-production environment where you can safely develop and test data, such as scripts, APIs, and commands. It is an investigation area that is not connected to a live (active) investigation.

To access the Playground, do one of the following:

* Go to **Investigation & Response** → Automation → **Playground**
* In any browser, type `https://<tenant>.<region>.paloaltonetworks.com/playground`

{% hint style="info" %}
### Tip

In the Playground, you can clear the context data, if needed, which deletes everything in the Playground context data, but does not affect the actual issue or case. To clear the context, run `!DeleteContext all=yes'` from the CLI or click **Clear Context Data** while viewing the context data.
{% endhint %}

### View War Room entries

When you open the War Room, you can see all the actions taken on a case, such as commands and notes in several formats such as Markdown, and HTML. When Markdown, HTML, or geographical information is received, the content is displayed in the relevant format.

To view specific data entries, you can filter entries by selecting the relevant checkbox, such as:

* **Chats**: Shows communication between team members.
* **Notes**: Any entries marked as notes.
* **Files**: Anything uploaded to the War Room in a playbook, script, or by the analyst.
* **Issue History**: Any issue field that was modified.
* **Commands and playbook tasks**: Any actions taken by playbook tasks or run manually by the analyst.
* **Tags**: Any tags added to the investigation.

{% hint style="info" %}
### Note

Cortex XSIAM does not index notes and chats.
{% endhint %}

In each War Room entry, you can take the following actions:

<table><thead><tr><th width="202">Action</th><th>Description</th></tr></thead><tbody><tr><td>Mark as note</td><td><p>Marks the entry as a note, which can help you understand why certain action was taken and assist future decisions.</p><p>You can also add a note by doing the following:</p><ul><li>Upload a file to the War Room by selecting <strong>Mark as Note</strong>.</li><li>If the <strong>Issue Overview</strong> tab includes a <strong>NOTES</strong> section, add it to the section.</li><li><p>In a playbook task (Advanced tab)</p><p>Tasks can be automatically added from script outputs as notes.</p></li><li><p>In the CLI by running the <code>!markAsNote entryIDs=&#x3C;``ID of the war room entry></code> command.</p><p>In the relevant War Room entry, click <strong>Copy to CLI</strong> to retrieve the <code>ID of the War Room entry</code>.</p></li></ul><p>When marked as a note, it is highlighted, so you can easily find them in the War Room or the <strong>Issue Overview</strong> tab.</p></td></tr><tr><td>View artifact in new tab</td><td>Opens a new tab for the artifact.</td></tr><tr><td>Detach from task</td><td>Removes a task from the artifact.</td></tr><tr><td>Attach to a task</td><td>Adds a task to the artifact.</td></tr><tr><td>Add tags</td><td>Add any relevant tags to use that help you find relevant information.</td></tr><tr><td>Copy to CLI</td><td><ul><li>ID: Entry IDs are used to uniquely identify War Room entries and take the format <code>&#x3C;ENTRY_IDENTIFER>@&#x3C;CASE_ID></code>, for example, <code>54925dc3-a972-4489-8bef-793331fa6c77@1</code>. Many out-of-the-box commands and scripts use entry IDs arguments to pass in files as inputs.</li><li>URL: Copy the URL which is a direct link to the War Room entry</li></ul><p>To find the entry ID or URL of an entry in the War Room, click on the vertical ellipsis icon at the upper right of the entry, then copy the value.</p></td></tr></tbody></table>

### Run commands in the War Room CLI

You can run system commands, integration commands, and scripts from an integrated command line interface (CLI), which enables you to make comments in your case (in plain text or Markdown) and to execute automation scripts, system commands, and integration commands. This gives SOC teams the power to execute automations ad-hoc to support their investigations or make notes as they investigate cases.

In the CLI, you can run various commands by typing the following:

<table><thead><tr><th width="110">Action</th><th>Description</th></tr></thead><tbody><tr><td><code>!</code></td><td>Runs integration commands, scripts, and built-in commands, such as adding evidence and assigning an analyst.</td></tr></tbody></table>

You can find relevant commands, scripts, and arguments with the CLI’s auto-complete feature. This also includes fuzzy searching to help you find relevant commands based on keywords. If you type the exclamation mark (**!**) and start typing, autocomplete populates with options that might suit your needs. For example, if you want to work with tasks, type `!task`, and all commands and scripts that include the `task` in their name will display.

\{% hint style="info" %\} Tip: Use the up/down arrow keys in the CLI to search command history. This searches previous commands with the same prefix. \{% endhint %\}

<details>

<summary>Special characters</summary>

| Characters                                 | Description                                                                                                  |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| `&&, \|\|, !, {, }, [, ], (, ), ~, *, ?`   | To use these characters, place them within single or double quotes. An escape character `\` is not required. |
| `\, \n, \t, \r, ", ^, :,` comma, and space | To use these characters, place them within single or double quotes and use an escape character `\`.          |

</details>

<details>

<summary>Common arguments</summary>

The following common arguments are available for every script run from the CLI.

<table><thead><tr><th width="198">Argument Name</th><th>Description</th></tr></thead><tbody><tr><td>auto-extract</td><td><p>Whether/when to extract indicators. Possible values:</p><ul><li><code>inline</code>: Extracts indicators within the indicator extraction run context (synchronously).</li><li><code>outofBand</code>: Extracts indicators in parallel (asynchronously) to other actions.</li><li><code>none</code>: Does not extract indicators (recommended for scripts with large outputs when indicator extraction is not required).</li></ul></td></tr><tr><td>execution-password</td><td>Supplies a password to run a password-protected script.</td></tr><tr><td>execution-timeout</td><td>Defines how long a command waits in seconds before it times out.</td></tr><tr><td>extend-context</td><td><p>Select which information from the raw JSON you want to add to the context data.</p><p>For a single value: <code>contextKey=RawJsonOutputPath</code></p><p>For multiple values: <code>contextKey1=RawJsonOutputPath1::contextKey2=RawJsonOutputPath2</code></p></td></tr><tr><td>ignore-outputs</td><td>Possible values: <code>true</code> or <code>false</code>. If set to <code>true</code>, it does not store outputs in the context (besides extend context).</td></tr><tr><td>raw-response</td><td>Possible values: <code>true</code> or <code>false</code>. If set to <code>true</code>, it returns the raw JSON result from the script.</td></tr><tr><td>retry-count</td><td>Determines how many times the script attempts to run before generating an error.</td></tr><tr><td>retry-interval</td><td>Determines the wait time (in seconds) between each script execution.</td></tr><tr><td>using</td><td>Selects which integration instance runs the command.</td></tr><tr><td>using-brand</td><td>Selects which integration runs the command. If the selected integration has multiple instances, the script may run multiple times. Use the <code>using</code> argument to select a single integration instance.</td></tr><tr><td>using-category</td><td>Selects which category of integrations runs the command. If the selected category includes multiple integration instances, the script may run multiple times. Use the <code>using</code> argument to select a single integration instance.</td></tr></tbody></table>

</details>

<details>

<summary>Access attributes in the Unified Asset Inventory</summary>

{% hint style="info" %}
**License type:** This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

Commands you run in the War Room can automatically populate parameters such as region, account id, and tags, based on asset data. Commands can reference UIA attributes for the relevant asset(s) in the issue context and use those attributes as input. The issue must contain the relevant `Asset ID`.

The syntax to reference attributes in the UAI is `${asset.xdm.asset.attributename}`. To find the property path in the XDM data set, see the asset data card for the asset in the **Inventory** page. For example, to print the region for the asset, enter `!print value=${asset.xdm.asset.cloud.region}`. You can also run commands and scripts directly on the asset using `${asset.xdm.asset}`.

</details>

<details>

<summary>Run commands in the Automations browser</summary>

You can view and run commands and scripts (not system commands, operations, and notifications) in the **Automations Browser**, by clicking <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-2a806a53827b323b5762ed4191b52e491b0fd022%2F2bda57c0f3a5727da391846f02c35d67c0c63a25f63cafd7c7b39705c620991e.png?alt=media" alt="exclamation-cli.png" data-size="line"> next to the CLI.

The **Automations Browser** enables you to run commands and all associated arguments. The scripts and commands are separated into sections such as scripts and built-in commands. In each argument, you can do the following:

* Hardcode the value
*   Use a dynamic value

    You can dynamically pass information into the argument by clicking the curly bracket. For example, the `EmailAskUser` command asks a user a question via email. In the `email` argument, rather than typing the user's email address, you can send it to whoever created the case.

    1. In the **email** field, click the curly brackets.
    2. In the search box, enter `created`.
    3.  Under **CASE DETAILS** click **Created by**.

        The email argument appears as `${alert.dbotCreatedBy}`.
    4.  Run the command.

        An email is sent to the user who created the case.

    You can use transformers and filters to filter and transform data from the command.

</details>

<details>

<summary>Common arguments when using the Automations browser</summary>

<table><thead><tr><th width="198">Argument</th><th>Description</th></tr></thead><tbody><tr><td>Using</td><td>Selects which integration instance runs the command.</td></tr><tr><td>Extend context</td><td><p>Determines the wait time (in seconds) between each script execution.</p><p>For a single value: <code>contextKey=RawJsonOutputPath</code></p><p>For multiple values: <code>contextKey1=RawJsonOutputPath1::contextKey2=RawJsonOutputPath2</code></p></td></tr><tr><td>Ignore outputs</td><td>Does not store outputs in the context (besides extend context).</td></tr><tr><td>Execution timeout (seconds)</td><td>Defines how long a command waits in seconds before it times out.</td></tr><tr><td>Number of retries</td><td>Determines how many times the script attempts to run before generating an error.</td></tr><tr><td>Retry interval (seconds)</td><td>Determines the wait time (in seconds) between each script execution.</td></tr></tbody></table>

</details>

<details>

<summary>Examples using the CLI</summary>

To run the print script with a value of `"hello"` and the key `a` from the context:

`!Print value="hello ${a}"`

To run the Python command returning Hello World using escape characters:

`!py script="demisto.results(\"hello world\")"`

To run the Python command returning Hello World using backticks:

`` !py script=`demisto.results("hello world")` ``

</details>
