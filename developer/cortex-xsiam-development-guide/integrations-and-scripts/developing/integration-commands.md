---
description: Cortex XSIAM integration command design, arguments, and outputs.
---

# Integration commands

In addition to fetching incidents or indicators, your integration can map product APIs in commands that you want to expose to Cortex XSIAM.

Every command takes inputs (arguments) and returns outputs.

Command names follow a naming convention that makes it easy for users to understand their function: `!vendor-object-action`. Use [kebab-case](https://medium.com/better-programming/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841) for command names. For example, a command of an integration from vendor HelloWorld that performs an update action of an object of type alert, should be named: `!helloworld-alert-update`.

Integration commands are used in two ways in Cortex XSIAM:

* Playbooks - integration commands can be used for playbook tasks.
* CLI - users can manually run commands within an incident using the Cortex XSIAM CLI by typing `!commandname` and specifying the arguments.

Customers typically use a combination of both methods. They use commands to automate processes through playbooks. When they are conducting manual investigations, they run commands from the CLI to analyze the data.

It is important to understand how arguments and outputs work in Cortex XSIAM and to understand design best practices.

### Cortex XSIAM integration command design

Commands should ideally run a single API call to your product. This simplifies the handling of conditions where some calls fail and others succeed. Whenever possible such logic should be implemented in playbooks rather than in integrations.

Verify that commands run quickly and are non-blocking. A command should never take more than 2 to 3 seconds to run and return the information, or it can have significant performance impacts in Cortex XSIAM.

{% hint style="info" %}
**Important**

Do not use sleep() in your code. If you have commands that need to run for longer periods of time, there are two options:

* Make the commands asynchronous and implement a [generic polling](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/) mechanism, as used in the [HelloWorld](https://github.com/demisto/content/blob/master/Packs/HelloWorld/Integrations/HelloWorld/HelloWorld.py) integration. For example, if you need to run a search across your endpoints, instead of a single command that waits until the search is completed, you should implement three separate commands.
  * A command that triggers the search and returns immediately a job ID as output. For example, `!helloworld-start-scan`.
  * A command that checks the status of the job taking the job ID as input. For example, `!helloworld-scan-status`.
  * A command that retrieves the results of a job when it's complete, taking the job ID as input. For example, `!helloworld-scan-results`.
* Use [long running containers](../advanced-topics/long-running-containers). This is suitable for services that need to keep a connection open for a long time or need to open a listening TCP port. For example, Slack.
{% endhint %}

In some cases you want to build commands that perform generic well-known actions that are common across several use cases. For example, reputation commands that return enrichment and reputation information about indicators, such as IPs. For those scenarios, we have standardized ways to define command names, inputs and outputs that make interoperability easier. For more information, see [Generic commands](generic-commands) and [DBotScore](reputation-and-dbot-score).

### Cortex XSIAM integration command arguments

Arguments are the inputs of your integration commands. They can be mandatory or optional, and can have default and predefined values. For more information, see the commands section of the [Metadata YAML file](../components/integration-metadata-yaml-file) documentation.

Command arguments should be named using [snake\_case](https://medium.com/better-programming/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841).

When you design commands and their inputs, keep in mind how they are invoked. If a user, either manually or through a playbook, has to provide an input, where do they get that input data from? Is it an input they are likely to know? Or the output of another command?

We recommend making the argument values consistent with what the user needs to provide in the user interface of the original product you are integrating with, not necessarily with what the API requires. For example, if in the product UI you have three options for an argument: `Low`, `Medium` and `High`, but the product API takes corresponding numbers (`1`, `2` and `3`), then your integration's command argument should support `Low`, `Medium` and `High` and you should take convert the argument values to numbers in your integration code. The user experience of the integration should be consistent with what the user is already familiar with.

Another important design rule is to avoid having the SOC analyst waste time and focus by switching across multiple consoles to retrieve data from many different places. If they need to provide an input value in a command, there should be a way to get that information from within Cortex XSIAM.

For example, imagine that you are designing a command that modifies an existing firewall policy. For simplicity, assume you have only two arguments: the ID of the policy and the action (allow or deny). The latter argument is obvious: depending on what the user wants to do, they will set the value to allow or deny (you can set predefined values so the user can only choose between these two options). But what about the ID of the policy? It may not be something that they know. They may know the policy name, but you don't want them to switch context and log in to a different console to find the ID that corresponds to the name. In this case, design your integration to include a command that returns a list of all policies and shows their IDs, or allows the user to retrieve the ID from the name, so that the user doesn't have to switch consoles.

### Cortex XSIAM integration command outputs

Every automation script and integration command returns several types of outputs:

*   Human readable

    Human readable output is shown to the user in the War Room and is typically formatted in a way that is understandable by the SOC analyst. The human readable data is usually a subset of the entire information returned by your command. In most cases, you show the most relevant data that is also present in the user interface of the product you are integrating with. The ordering is important, display the most relevant fields (and the ones the user is most familiar with) in the leftmost columns.
*   Context data

    Outputs are also saved in a structured format (JSON backed) within an incident, so they can be retrieved later and used as inputs of other tasks (either within playbooks or from the CLI).

    The context stores the results from every integration command and every automation script that is run. Whether you run an integration command from the CLI or from a playbook task, the output result is stored into the JSON context in the incident or the playground. When you run a command such as `!whois query="cnn.com"` the data is returned and the results stored in the context.
* Additional outputs such as images or files.

When you design your outputs, the data must be properly formatted for both human consumption and machine consumption. The following are best practices for outputs:

* Keep human readable information to the reasonable minimum. Remove data that is not relevant to a human analyst and present the remaining data in an orderly manner. We recommend using tableToMarkdown() to automatically format lists into tables. The tableToMarkdown() function also supports arguments that allow you to filter and order columns and improve the formatting of the column headers.
* Keep context data organized:
  * Return data using a prefix, such as `VendorName.Entitytype`. For example, if your Pack is called `HelloWorld` and you are returning a list of hosts, the prefix of the output should be `HelloWorld.Host`.
  * Use the [CommandResults](python-code-conventions) class to return data to make sure it's properly formatted, and use the `outputs_key_field` parameter to identify the primary keys.
  * Adhere to the [Standard Context](context-standards).

More information is available about [context and outputs](context-and-outputs).

If you are returning files, it's important to understand the difference between `Files` and `InfoFiles`, as you should specify the right return type in your command output:

* `Files` are potentially malicious files (i.e. attachments from potential phishing emails) that should be treated as such. They are automatically enriched (by checking their reputation against configured threat intel sources) and detonated in sandboxes. For more information, see the **File** section of the [Mandatory context standards](../context-standards#UUID-57b3a4f0-fd98-9b0f-af6e-aa954c13889d) topic.
* `InfoFiles` are not malicious by definitions. They can be reports, CSVs, and other artifacts that your API returns. They are not automatically enriched and detonated. For more information, see the **InfoFile** section of the [Mandatory context standards](../context-standards#UUID-57b3a4f0-fd98-9b0f-af6e-aa954c13889d) topic.

### Built-in Cortex XSIAM filters and commands

Use the following built-in elements to facilitate your investigation and response.

<details>

<summary>getEntries filter</summary>

When building a script, you can fetch entries from an incident. If you do not specify the incident ID number, the script fetches from the current incident. You can create a filter to limit the search results.

| Filter          | Description                                                                                                                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pageSize        | The number of entries to return.                                                                                                                                                                               |
| lastId          | Return entries starting from the specified entry ID and backward.                                                                                                                                              |
| firstID         | Return entries starting from the specified entry ID and forward.                                                                                                                                               |
| selectedEntryID | Return entries before and after the specified entry ID.                                                                                                                                                        |
| categories      | Return entries with the specified categories (array). {commandAndResults, playbookTaskResult, playbookTaskStartAndDone, playbookErrors, justFound, deleted, incidentInfo, chats, evidence, notes, attachments} |
| tags            | Return entries with the specified tags (array).                                                                                                                                                                |
| users           | Return entries with the specified users (array).                                                                                                                                                               |
| tagsAndOperator | Return entries that include all specified tags.                                                                                                                                                                |
| fromTime        | Return entries from this time and forward.                                                                                                                                                                     |
| parentID        | The ID of the parent entry.                                                                                                                                                                                    |

#### Get entries marked as notes

```programlisting
res = demisto.executeCommand("getEntries", {"filter": {"categories": ["notes"]}})
demisto.results(str(res))
```

Response

```programlisting
[{
        u 'Category': u 'Builtin',
        u 'ModuleName': u 'InnerServicesModule',
        u 'System': u '',
        u 'Note': True,
        u 'Version': 2,
        u 'ReadableContentsFormat': u '',
        u 'Type': 1,
        u 'Metadata': {
            u 'reputationSize': 0,
            u 'startDate': u '0001-01-01T00:00:00Z',
            u 'recurrent': False,
            u 'sortValues': None,
            u 'file': u '',
            u 'retryTime': u '0001-01-01T00:00:00Z',
            u 'previousAllReadWrite': False,
            u 'endingDate': u '0001-01-01T00:00:00Z',
            u 'id': u '96@42646',
            u 'contents': u '',
            u 'cronView': False,
            u 'category': u 'chat',
            u 'note': True,
            u 'isTodo': False,
            u 'format': u 'markdown',
            u 'system': u '',
            u 'mirrored': False,
            u 'hasRole': False,
            u 'pinned': False,
            u 'instance': u 'Builtin',
            u 'version': 2,
            u 'parentId': u '',
            u 'type': 1,
            u 'brand': u 'Builtin',
            u 'timezoneOffset': 0,
            u 'scheduled': False,
            u 'parentEntryTruncated': False,
            u 'previousRoles': None,
            u 'allRead': False,
            u 'allReadWrite': False,
            u 'incidentCreationTime': u '0001-01-01T00:00:00Z',
            u 'ShardID': 0,
            u 'reputations': None,
            u 'user': u 'admin',
            u 'taskId': u '',
            u 'parentContent': u '!getEntries filter="{\\"categories\\":[\\"notes\\"]}"',
            u 'fileMetadata': None,
            u 'tags': None,
            u 'tagsRaw': None,
            u 'errorSource': u '',
            u 'entryTask': None,
            u 'roles': None,
            u 'created': u '2021-03-08T18:47:47.786120529Z',
            u 'IndicatorTimeline': None,
            u 'modified': u '2021-03-08T18:47:51.032485206Z',
            u 'times': 0,
            u 'investigationId': u '42646',
            u 'dbotCreatedBy': u 'admin',
            u 'playbookId': u '',
            u 'contentsSize': 14,
            u 'previousAllRead': False,
            u 'fileID': u ''
        },
        u 'ContentsFormat': u 'markdown',
        u 'Tags': None,
        u 'Brand': u 'Builtin',
        u 'HumanReadable': None,
        u 'ID': u '96@42646',
        u 'FileID': u '',
        u 'IgnoreAutoExtract': False,
        u 'IndicatorTimeline': None,
        u 'Evidence': False,
        u 'EntryContext': None,
        u 'Contents': u 'This is a note',
        u 'File': u '',
        u 'EvidenceID': u '',
        u 'FileMetadata': None,
        u 'ImportantEntryContext': None
    }
]
```

</details>

<details>

<summary>taskComplete command</summary>

Use this command to mark a playbook task as completed. For example, you might need to include the `taskComplete` command in a SLA breach script, to close a task and force the playbook to continue running after the SLA has been breached. You can also use the `taskComplete` command to add an action button in an incident layout, that can be used to mark a specific playbook task as complete.

| Argument         | Description                                                                                                                                                                                                                               |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id               | Specify the task ID or tag to complete.                                                                                                                                                                                                   |
| parentPlaybookID | Parent playbook task ID, limits task identification by tags to this sub-playbook only.                                                                                                                                                    |
| incdientId       | Incident ID this task belongs to. Defaults to current incident.                                                                                                                                                                           |
| comment          | Task completion comment.                                                                                                                                                                                                                  |
| input            | Conditional task completion selection.                                                                                                                                                                                                    |
| allowSkipped     | Allow performing actions on skipped tasks (default is Yes).                                                                                                                                                                               |
| isAutoRun        | When set to `True`, the task is executed. Default is `False`. Relevant only for script/playbook tasks. When set to `False`, the task is completed immediately.                                                                            |
| args             | Set only if `isAutoRun=true`. Passing input arguments to the task script/playbook for execution. The args must be JSON format where the key is the name of the script/command/playbook argument name. Example: `{"ARG_NAME":"ARG_VALUE"}` |

</details>

<details>

<summary>reopenInvestigation command</summary>

Use this command to reopen a closed incident. For example, you can use the `reopenInvestigation` command to add an action button in the incident layout that can reopen a closed incident and take a specific action, such as rerunning the incident's playbook. You can also include the `reopenInvestigation` command in a loop in a script to reopen multiple incidents.

| Argument | Description                                                                                |
| -------- | ------------------------------------------------------------------------------------------ |
| id       | Which incident to reopen. If no incident ID is provided, the current incident is reopened. |

</details>
