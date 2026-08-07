---
description: >-
  Use commands to schedule the future execution of other commands in playbook
  tasks.
---

# Scheduled Commands

A command can schedule the future execution of another command. In playbook tasks using scheduled commands, the task does not proceed to the next task until it is done with all scheduled commands and there is no future execution scheduled. When a playbook waits for a command execution, it does not use a worker, since workers are only used at the time commands are executed.

You can use scheduled commands in a polling flow when a command cannot return the full result in a single execution (for example, when a remote process hasn't finished execution). Scheduled commands enable you to try the command again later and return the full results when available. For an example, see [Cortex XDRIR Endpoint Isolation](https://xsoar.pan.dev/docs/reference/integrations/cortex-xdr---ir#xdr-endpoint-isolate).

**YAML prerequisite**

* Integration - in the integration YAML, under the command root, add `polling: true`.
* Script - in the script YAML, in the root of the file, add `polling: true`

**The polling\_function decorator**

The `polling_function` decorator can be used to avoid much of the code you would otherwise need to implement to write a polling function.

All functions implementing this decorator must always return a `PollResult` object.

{% hint style="info" %}
### Note

Args must be the first parameter in the function definition and call.
{% endhint %}

**polling\_function decorator code example**

In the example below, we are polling against the `client.call_api` function. If the API has a successful response, we return our results wrapped in a `PollResult` object. If the response is not successful, we return whether to `continue_to_poll` according to the results of the `should_not_keep_polling` function. A Boolean or a predicate can be passed to `continue_to_poll`

```programlisting
@polling_function('cs-falcon-sandbox-result')
def some_polling_command(args: Dict[str, Any], client: Client):
    key = get_api_id(args)
    api_response = client.call_api()
    successful_response = api_response.status_code == 200

    if successful_response:
        success_return = show_successful_response()
        return PollResult(success_return)

    else:
        error_response = CommandResults(raw_response=report_response,
                                        readable_output='API returned an error',
                                        entry_type=entryTypes['error'])

        return PollResult(continue_to_poll=lambda: not should_not_keep_polling(client, key), response=error_response)
```

**polling\_function arguments**

| Arg                    | Type | Description                                                               | Default           |
| ---------------------- | ---- | ------------------------------------------------------------------------- | ----------------- |
| name                   | str  | The name of the command.                                                  | Not applicable    |
| interval               | int  | How many seconds until the next run.                                      | 30                |
| timeout                | int  | How long to poll until timeout.                                           | 600               |
| poll\_message          | str  | The message to display in the war room while polling.                     | Fetching Results: |
| polling\_arg\_name     | str  | The name of the argument to indicate polling should be done.              | polling           |
| requires\_polling\_arg | bool | Whether a polling argument should be expected as one of the demisto args. | True              |

**PollResult class**

| Arg                  | Type                    | Description                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| response             | any                     | The response of the command in the event of success, or in case of failure but Polling is false.                                                                                                                                                                                                                                                                                                              |
| continue\_to\_poll   | union \[bool, Callable] | Whether to return a `ScheduledCommand` to the server to keep polling.                                                                                                                                                                                                                                                                                                                                         |
| args\_for\_next\_run | dict                    | <p>The arguments to use in the next iteration. Will use the input args in case of <code>None</code>.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If you are using this argument, you must add it to the YAML file with the attribute "hidden: true", so that the polling command recognizes the argument for the next run.</p></div> |
| partial\_result      | CommandResults          | `CommandResults` to return, even though we will poll again.                                                                                                                                                                                                                                                                                                                                                   |

{% hint style="info" %}
### Note

To ignore scheduled War Room entries, add `hide_polling_output` as a Boolean argument to the command in the YAML file. For an example, see the [cs-falcon-sandbox-scan](https://github.com/demisto/content/blob/849fee1dfe10907158e5c307dd367284accee2a0/Packs/CrowdStrikeFalconSandbox/Integrations/CrowdStrikeFalconSandboxV2/CrowdStrikeFalconSandboxV2.yml#L65) command.
{% endhint %}

**Advanced example**

In this example, we are trying to implement a command that submits a URL for analysis and then polls for the result. The proper way to implement this is to split the flow into two commands, the `submit` command and the `find` command. The `find` command is a polling command, and is useful on its own without the context of `submit`. We want to perform the `submit` command once and poll on the `get_result` command until we have a response. We will then have the `submit-file` command call the `find-url` command.

```programlisting
@polling_function('find-url')
def find_url_command(args: Dict[str, Any], client: Client):
    api_response = client.call_api(args.get('url')
    successful_response = api_response.status_code == 200

    if successful_response:
        success_return = show_successful_response(api_response)
        return PollResult(success_return)

    else:
        error_response = CommandResults(raw_response=report_response,
                                        readable_output='API returned an error',
                                        entry_type=entryTypes['error'])

        return PollResult(continue_to_poll=True, response=error_response)
        
def submit_url_command(args: Dict[str, Any], client: Client):
    client.submit_url(args.get('url))
    return find_url_command(args, client)
```

**ScheduledCommand class**

For scenarios the `polling_function` decorator does not cover, you can use the `ScheduledCommand` class for more advanced control over polling. `ScheduledCommand` is an optional class that enables scheduling commands via the command results.

| Arg                             | Type | Description                                                                                                                                                                                 |
| ------------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| command                         | str  | The command that runs after `next_run_in_seconds` has passed.                                                                                                                               |
| next\_run\_in\_seconds          | int  | <p>How long to wait before executing the command.</p><p>The interval between each run is determined by <code>next_run_in_seconds</code>, however it will never be less than 10 seconds.</p> |
| args (optional)                 | dict | Arguments to use when executing the command.                                                                                                                                                |
| timeout\_in\_seconds (optional) | int  | Number of seconds until the polling sequence timeouts.                                                                                                                                      |

When provided to `CommandResults` it transforms the result into a **schedule result**. After the next\_run\_in\_seconds delay, the command will be executed. The scheduled command can return another **schedule result** that schedules another scheduled command and so on.

The schedule sequence completes when any one of three terminating actions occur:

* Done: The integration finishes a schedule sequence by not returning a schedule result. Otherwise, the sequence continues as long as a schedule result is returned.
* Error: The schedule sequence finishes with an error when a command in the sequence returns an error result.
* Timeout (automatically handled): The schedule sequence finishes execution with a timeout error when the timeout is reached. Cortex XSIAM returns the timeout error entry automatically.

**Polling Scripts and ScheduledCommand**

When a script with polling: true is re-run because it still has work to do (for example, `items_remaining > 0`), it ignores any new arguments you try to pass it. Instead, it re-runs with the original arguments from the very first time the script was executed in that sequence. This behavior is by design for polling scripts, which are meant to repeatedly check on a single, long-running task. The system assumes you want to keep checking on the same task with the same initial parameters. If you need to pass new information or manage different stages of a task, the best and most reliable way to do this is to store the data in the incident context. This ensures your script can access and update the necessary information throughout its different runs, regardless of the polling logic.

**How to Ignore Scheduled War Room Entries**

You can prevent printing the `Scheduled Entries` to the War Room when there is no output. However, this is possible only for entries that are subsequent to the first entry, since the first entry is expected to provide context about the expected final result. This means the first entry is always expected to have a result, but the entries that come after it may be empty until a non-scheduled result is returned.

It is recommended to prevent printing to the War Room until the final result is available, since the schedule icon provides the scheduling context via its tooltip . To prevent War Room entries while using a `ScheduledCommand`, return a `CommandResults` with just a `scheduled_command`.

For example: `return_results(CommandResults(scheduled_command=scheduled_command))`

**Polling scripts with ScheduledCommand example**

In the following example, if the `status` is not `complete` then a result with `scheduled_command` is returned. After `interval_in_seconds` seconds (60 by default), the result schedules a poll for the search status and result. This is done in the next run as well, and repeats until the status is complete.

```programlisting
def run_polling_command(args: dict, cmd: str, search_function: Callable, results_function: Callable):
    interval_in_secs = int(args.get('interval_in_seconds', 60))
    if 'af_cookie' not in args:
        # create new search
        command_results = search_function(args)
        outputs = command_results.outputs
        af_cookie = outputs.get('AFCookie')
        if outputs.get('Status') != 'complete':
            polling_args = {
                'af_cookie': af_cookie,
                'interval_in_seconds': interval_in_secs,
                'polling': True,
                **args
            }
            scheduled_command = ScheduledCommand(
                command=cmd,
                next_run_in_seconds=interval_in_secs,
                args=polling_args,
                timeout_in_seconds=600)
            command_results.scheduled_command = scheduled_command
            return command_results
        else:
            # continue to look for search results
            args['af_cookie'] = af_cookie
    # get search status
    command_results, status = results_function(args)
    if status != 'complete':
        # schedule next poll
        polling_args = {
            'af_cookie': args.get('af_cookie'),
            'interval_in_seconds': interval_in_secs,
            'polling': True,
            **args
        }
        scheduled_command = ScheduledCommand(
            command=cmd,
            next_run_in_seconds=interval_in_secs,
            args=polling_args,
            timeout_in_seconds=600)

        # result with scheduled_command only - no update to the war room
        command_results = CommandResults(scheduled_command=scheduled_command)
    return command_results
```

**How to use with demisto.executeCommand**

When using `demisto.executeCommand()` a command or a script that returns a **schedule result** will not schedule a command execution. However, its result will contain the schedule metadata.

We recommend creating a new result with the `ScheduledCommand` class to schedule a future script execution.

Advanced users can extract the schedule metadata, and use it when scheduling the future script execution. The schedule metadata fields are: `PollingCommand`, `NextRun`, `Timeout`, and `PollingArgs` (for more information, see `return_results` in [Python code conventions](../developing/python-code-conventions)).

**demisto.executeCommand example**

For the `autofocus-search-samples` command that may return a **schedule result** (if it has `Metadata.polling` in its fields and `af_cookie` in its `Contents`) or a non-scheduled result, the wrapping script `AutoFocusSearchScript` can handle it as follows.

```programlisting
args = demisto.args()
samples_result = demisto.executeCommand('autofocus-search-samples', **args)
script_results = []
if samples_result and not isError(samples_result[0]):
    if demisto.get(samples_result[0], 'Metadata.polling'):  # result has polling metadata
        # extract the af_cookie from the results
        af_cookie = demisto.get(samples_result[0], 'Contents.AFCookie')
        if not af_cookie:
            raise ValueError('af_cookie is missing from schedule result.')
        schedule_args = {
            'af_cookie': af_cookie,
            'polling': True
        }
        schedule_command = 'AutoFocusSearchScript'
        # take the timeout and next_run from the polling fields
        schedule_timeout = demisto.get(samples_result[0], 'Timeout')
        schedule_next_run = demisto.get(samples_result[0], 'NextRun')
        scheduled_command = ScheduledCommand(
            command=schedule_command,
            next_run_in_seconds=int(schedule_next_run),
            args=schedule_args,
            timeout_in_seconds=int(schedule_timeout)
        )
        readable_output = "Autofocus search created successfully."
        script_results.append(CommandResults(
            readable_output=readable_output,
            scheduled_command=scheduled_command
        ))
    else:
        readable_output = "Autofocus search is done, see result below."
        script_results.append(CommandResults(readable_output=readable_output))
        script_results.extend(samples_result)
return_results(script_results)
```
