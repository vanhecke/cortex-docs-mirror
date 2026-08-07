# Configure a playbook to run timers

Within a playbook, you can set a timer to start, pause, or stop at a specific section header or task. For example, you can create a timer called Pending user response and have it start in a playbook when an email is sent to a user. If the user does not respond within the target timeframe, then you can automatically send an additional reminder to the user or run a different task.

To select a timer in a task or section header, in the Timers tab select the action that you want the timer to perform for the task. You can add multiple timers to a task or section header, so in the same task you can stop one timer and start another.

{% hint style="info" %}
When a task or section has a timer configured, it displays the hourglass icon.
{% endhint %}

The following table describes the timer options:

<table><thead><tr><th width="190">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>Timer.start</code></td><td><p>Starts the timer.</p><div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Timers are not started automatically when a case is created.</p></div></td></tr><tr><td><code>Timer.pause</code></td><td>Pauses the timer. A paused timer can be started again without being reset.</td></tr><tr><td><code>Timer.stop</code></td><td><p>Stops the timer. Information about the timer is still displayed in the issue layout and/or issues table, but the status displays as Ended.</p><div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>If you stop a timer before the issue is closed, you must reset the timer using the <code>resetTimer</code> command before you can start the timer again. When you reset the timer, all fields are cleared.</p></div></td></tr></tbody></table>

Some playbooks, such as Phishing - Generic v3, come out-of-the-box with timer tasks included. If you need the same timers across use cases, create a sub-playbook based on your use case or conditions such as issue severity.

If you want to stop or pause a timer in a playbook, you can use an existing task or create a new section header/task. When you select Timer.stop, the run is considered finished and cannot be restarted without setting it to zero. If you plan to restart the timer, select Timer.pause so you do not lose the accumulated time. By default, all timers stop when the case closes.

<br>
