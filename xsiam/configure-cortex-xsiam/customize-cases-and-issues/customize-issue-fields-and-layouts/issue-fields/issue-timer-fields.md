---
description: >-
  Configure Cortex XSIAM issue timer fields to track response times, SLAs, risk
  thresholds, and timeout automation.
---

# Configure issue timer fields

Configure Cortex XSIAM issue timer fields to track issue response times, service-level agreements (SLAs), and timeout targets. Timer fields are disabled by default. To enable them, go to **Settings** → **Configurations** → **General** → **Server Settings** → **Issues**, then enable **Timer Field**.

Timer fields track reaction times and issue-level metrics. Use separate timers for different stages. For example, track time since the first playbook ran or time waiting for a user response. Timers appear in the **Issues** table and issue layouts.

Start, stop, or pause timer fields with a playbook, script, or the CLI.

Timer fields count up from the start of an action or task. They can also count down to a target. Configure a risk threshold to identify timers at risk.

Running timers show their total duration. At-risk timers show an at-risk status. Timed-out fields show the total duration and the time past the target.

Timer fields do not trigger actions automatically when they time out. Configure a timer script to run when a timeout occurs.

### Automate issue timer timeouts with scripts

Use scripts to act on timeouts, such as sending an email. Scripts can also change an issue field or parent case, such as its owner. Cortex XSIAM includes out-of-the-box scripts, or you can create your own. Scripts must use the `SLA` tag to work with timer fields. For more information, see [automate-changes-to-issue-fields-using-timer-scripts](automate-changes-to-issue-fields-using-timer-scripts "mention").

### Manage issue timers with the CLI

Use the `setIssue` command in the CLI to set or change issue timers. You can also use commands such as `startTimer`, `stopTimer`, and `pauseTimer`. For more information, see [user-issue-timer-field-commands-manually-in-the-cli](user-issue-timer-field-commands-manually-in-the-cli "mention").
