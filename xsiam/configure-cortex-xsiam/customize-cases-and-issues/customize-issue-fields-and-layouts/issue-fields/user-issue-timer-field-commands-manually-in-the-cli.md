---
description: >-
  Use Cortex XSIAM CLI commands to set, start, pause, stop, and reset issue
  timer fields and SLA targets.
---

# Use issue timer field commands  in the CLI

You can manage the timers for a specific issue by running commands manually in the CLI. By running CLI command you can to manage timers on a more granular level within specific issues when the need arises. For example, for a high severity issue you might need to decrease the response time.

<details>

<summary>Set timer fields in Cortex XSIAM</summary>

Use the `setIssue` command to set a specific issue due date, or to set a specific timer field in an issue. If you add the `sla` parameter to the command, it sets the time for the issue's due date. If you also add the `slaField` you set the timer for the issue field.

To change the Time to Assignment field target to 30 minutes in the current issue, run the following command:

```
!setIssue sla=30 slaField=timetoassignment
```

To change the timer to February 1, 2024, at 11.12 am, run the following command:

```
!setIssue sla=2024-02-01T11:12
```

{% hint style="info" %}
When defining the values for the `slaField` use the machine name for the field, which is lowercase and without spaces. You can check the machine name by editing the issue field.
{% endhint %}

</details>

<details>

<summary>Start or stop timer fields in Cortex XSIAM</summary>

Run the following commands in the CLI:

<table data-header-hidden><thead><tr><th width="189"></th><th></th></tr></thead><tbody><tr><td>Command</td><td>Description</td></tr><tr><td><code>startTimer</code></td><td><p>Starts the timer.</p><p>This command can also be used to restart a paused timer.</p><pre><code>!startTimer timerField=timetoassignnment
</code></pre><p><br></p><div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Timer fields are not started automatically when an issue is created unless run in a playbook.</p></div></td></tr><tr><td><code>pauseTimer</code></td><td><p>Pauses the timer.</p><p>Use this command when a timer field has already started.</p><pre><code>!pauseTimer timerField=timetoassignment
</code></pre><p><br></p></td></tr><tr><td><code>stopTimer</code></td><td><p>Stops the timer.</p><pre><code>!stopTimer timerField=timetoassignment
</code></pre><p><br></p><div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>After a timer field is stopped, before you can start the timer again you must reset the timer using the <strong>resetTimer</strong> command.</p></div><p>Timers are automatically stopped when an issue is closed.</p></td></tr><tr><td><code>resetTimer</code></td><td><p>Clears all fields for the timer.</p><p>This command must be used before restarting a timer that was stopped.</p><pre><code>!resetTimer timerField=timetoassignment
</code></pre><p><br></p></td></tr></tbody></table>

{% hint style="info" %}
When running commands in the CLI, you can specify the `alertID` to change the timer for a different issue.
{% endhint %}

</details>

<br>
