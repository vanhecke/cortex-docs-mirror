---
description: >-
  Configure Cortex XSIAM issue timer fields to track targets, risk thresholds,
  and timeout actions with scripts.
---

# Configure issue timer fields

You can create timer fields that display in the issues table and issue layouts. When you create an issue timer field, you have the option of providing a target for completion and also the option of triggering a script when the timer field has timed out (the target has passed).

If you set a target for a timer field, the Risk Threshold is automatically activated and displayed when the timer is considered at risk. You can customize the timeframe for the Risk Threshold. If you do not provide a target, the timer only counts up from when it was triggered.

You can start, stop, or pause a timer from the CLI, from scripts, and from playbooks.

### Create a timer issue field in Cortex XSIAM

1. Go to Settings → Configurations → Object Setup → Issues → Fields → New Field.
2. Select Timer as the Field Type.
3. Type a field name.
4.  (Optional) Under Basic Settings, Timer you have the option of setting a target for the timer field. By default, the timer field shows hours and minutes. You can change this to days and hours, by clicking Hours. If you do not enter the number of hours and minutes, the timer only counts up from when it is triggered.

    If you set a target in the timer field, by default the Risk Threshold field is activated. You can edit the Risk Threshold value.
5.  (Optional) Under Run script on timeout, select the script to run when the target has timed out. For example, you could write a script that sends an email when the target has timed out. For more information, see [Automate changes to issue fields using timer scripts](automate-changes-to-issue-fields-using-timer-scripts).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Only scripts to which you have added the <code>sla</code> tag appear in the list of scripts you can select. To add a tag to a script, create a new script or edit an existing script and enter the tag name in the script settings.</p><p>When you hover over the machine name (below the Field Name) note the name which is used in the command line or script.</p></div>
6. Save the field.
7. (Optional) Add the field to one or more issue layouts. By default, the timer field is available to view in the issues table.
