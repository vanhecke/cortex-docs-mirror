# Documentation best practices

This article describes the desired documentation standards in Cortex XSIAM content entities, and contains examples that can be useful when writing documentation.

{% hint style="info" %}
### Note

If you are writing documents for Cortex XSOAR and Cortex XSIAM that contains similar content, you can use special formatted strings that enable you to filter the correct entity. For more information, see [Cortex XSOAR and Cortex XSIAM Formatting](#cortex-xsoar-and-cortex-xsiam-formatting).
{% endhint %}

<details>

<summary>Entities Description Field</summary>

#### For playbook and scripts, use the following guideline:

* Should start with the verb that describes what the entity does.
* There is limited space for descriptions, do not use unnecessary words.

Before: `The XYZ playbook is a playbook that...`

After shortening the description: `Executes as a sub-playbook and enriches indicators from the list.`

Additional examples of concise descriptions:

* Investigates an access incident by gathering user and IP information, and handles the incident based on the stages in "Handling an incident - Computer Security Incident Handling Guide" by NIST.
* Blocks domains using Palo Alto Networks Panorama or Firewall External Dynamic Lists.
* Enables you to get all of the corresponding file hashes for a file even if there is only one hash type available.
* Uses generic polling to get saved question results.

#### For integrations:

The description should summarize all of the currently supported endpoints into a sentence that users can easily understand.

For example:

* Use the `IronDefense` integration to rate alerts, update alert statuses, add comments to alerts, and report observed bad activity.
* Use the `Gmail` integration to send/receive emails, manage user accounts, and listen to specified mailboxes and folders.

</details>

<details>

<summary>Fetch Incidents/Indicators section</summary>

Common parameters for this section are:

| Parameter name | Display name                                                                             |
| -------------- | ---------------------------------------------------------------------------------------- |
| First fetch    | First fetch timestamp (\<number> \<time uni>, e.g., 12 hours, 7 days, 3 months, 1 year). |
| Fetch size     | The maximum number of results to return per fetch. The default is 50.                    |

Any other important information needed for fetching incidents from the service should be added as a parameter.

Add documentation about the fetch function (especially the first fetch) that is not obvious from looking at the integration. This can be done in the [README](readme-files-for-content-entities) file or the [integration detailed description](../integrations-and-scripts/components/integration-description-file) file .

For example: `All incidents created in the minute prior to the configuration of Fetch Incidents and up to the current time will be imported.`

</details>

<details>

<summary>Common integration parameters</summary>

The most commonly used integration parameters:

| Parameter name | Display name                          | Notes                                                                                                                                                                                       |
| -------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API token/key  | API Token/ API Key/ API Secret.       | Provided by the third party integration.                                                                                                                                                    |
| URL            | Server URL                            |                                                                                                                                                                                             |
| insecure       | Trust any certificate (not secure)    | When ‘trust any certificate’ is selected, the integration ignores TLS/SSL certificate validation errors. Used to test connection issues or connect to a server without a valid certificate. |
| proxy          | Use system proxy settings             | Runs the integration instance using the proxy server (HTTP or HTTPS) that you defined in the server configuration.                                                                          |
| Threshold      | The minimum number/severity/score ... |                                                                                                                                                                                             |
| Limit          | The maximum number of...              |                                                                                                                                                                                             |

</details>

<details>

<summary>Parameters found in all integrations</summary>

| Parameter                                          | Notes                                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Run on Single engine / Run on Load Balancing Group | Communications between Cortex XSIAM and the third-party service are executed through the selected engine or load balancing group, not directly.                                                                                                                                                                                                                                                     |
| Do not use by default                              | <p>Use to avoid exceeding API quotas</p><ul><li>When enabled, commands from this integration are not available through the CLI, when you run a generic command that uses all available integration commands.</li><li>To use a command at the CLI from an instance with <code>do not use by default</code> enabled, you need to specify the instance with the <code>using</code> argument.</li></ul> |

</details>

<details>

<summary>Common command arguments</summary>

| Argument type                 | Description template                                                 | Example                                                                                                                                   |
| ----------------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Boolean                       | If `true`... If `false`... Default is `true`.                        | If `true`, return full results. If `false`, return partial results. Default is `true`.                                                    |
| String                        | The...                                                               | The user name of the user whose endpoint is being blocked.                                                                                |
| Integer                       | - The number of...\n - The total number of…\n - The maximum number\n | <p>- The number of times the script attempted to run. - The total number of matches.</p><p>- The maximum number of results to return.</p> |
| Array                         | A comma-separated list of                                            | A comma-separated list of IP addresses...                                                                                                 |
| List of predetermined options | The…. Can be “optionA”, “optionB”, or “optionC”.                     | The severity of the incident to fetch. Can be "Low", "High" or "Critical".                                                                |

</details>

<details>

<summary>Outputs</summary>

Try to be as specific as possible explaining what the output does.

For example, if the context path is: `Tripwire.Version.exists`

A poor description: `Exists of element versions.`

A good description: `True if the version of the element exists.`

| Argument type                 | Description template                                                                    | Example                                                                                                                                                     |
| ----------------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Boolean                       | If `true`... If `false`... Default is `true`.                                           | If `true`, will return full results. If `false`, will return partial results. Default is `true`.                                                            |
| String                        | The...                                                                                  | The user name of the user whose endpoint is being blocked.                                                                                                  |
| Integer                       | <p>- The number of...\n</p><p>- The total number of…\n</p><p>- The maximum number\n</p> | <p>- The number of times the script attempted to run.</p><p>- The total number of matches.</p><p>- The maximum number of results to return.</p>             |
| Array                         | A comma-separated list of                                                               | A comma-separated list of IP addresses...                                                                                                                   |
| List of predetermined options | The…. Can be “optionA”, “optionB”, or “optionC”.                                        | The severity of the incident to fetch. Can be "Low", "High" or "Critical"                                                                                   |
| Unknown                       | <p>- An array of...\n - A list of…\n</p><p>-A dictionary of...</p>                      | A list of indicators associated to..                                                                                                                        |
| Date                          | <p>- The date and time that...\n</p><p>- The date and time when...</p>                  | The date and time when the indicator was last updated. The date format is: YYYYMMDDThhmmss, where "T" denotes the start of the value for time, in UTC time. |

</details>

<details>

<summary>Cortex XSOAR and Cortex XSIAM formatting</summary>

Rather than creating separate documents, you can add the following format to the release notes, Description.md or README.md documents:

| Format                   | Description                   |
| ------------------------ | ----------------------------- |
| <\~XSOAR>Text\</\~XSOAR> | Applies to Cortex XSOAR only. |
| <\~XSIAM>Text\</\~XSIAM> | Applies to Cortex XSIAM only. |

In this example, we only want to show Cortex XSOAR text:

```programlisting
<~XSOAR>Some XSOAR text</~XSOAR>
<~XSIAM>Some XSIAM text</~XSIAM>
<~XSOAR>XSOAR</~XSOAR><~XSIAM>XSIAM</~XSIAM> is the best.
```

When the pack is deployed in the the Cortex XSOAR marketplace the generated file will only have the following:

```programlisting
Some XSOAR text
XSOAR is the best.
```

And in the Cortex XSIAM marketplace like this:

```programlisting
Some XSIAM text
XSIAM is the best.
```

</details>
