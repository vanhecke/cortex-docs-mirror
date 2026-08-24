---
description: >-
  Troubleshoot Cortex XSIAM playbook performance, identify slow workflow tasks,
  and analyze execution data with XQL.
---

# Troubleshoot playbook performance

Analyze Cortex XSIAM playbook metadata, including task inputs, outputs, storage use, and task types. Use this data to troubleshoot custom playbook performance, high CPU use, memory consumption, or disk usage.

### Analyze playbook performance with XQL datasets

Use XQL to track Cortex XSIAM playbook and script performance. XQL provides execution data for debugging, queries, and dashboards. The following datasets are available:

* playbook\_tasks: Data about failed tasks and tasks that were retried.
* playbook\_runs: Data about playbook runs and statuses.
* scripts\_and\_commands\_metrics: Data about scripts and commands used in playbook tasks.

### Get Cortex XSIAM playbook metadata using the CLI

After an issue has been assigned to a playbook you can analyze it to see its tasks inputs/outputs storage. You can filter the data according to the KB used in each task input/output.

From the **Cases & Issues** → **Cases** page, in the **Case War Room** tab the following command in the CLI.

`!getInvPlaybookMetaData issueId=`_`<issue ID>`_` `` ``minSize= `_`<size of the data you want to return in KB. Default is 10>`_

To view the playbook metadata that is used in issue number 964, in the CLI type `!getInvPlaybookMetaData incidentid=”964” minSize=”0”!getInvPlaybookMetaData incidentid=”964” minSize=”0”.`

### Use the Troubleshooting Playbooks dashboard

From the **Troubleshooting Playbooks** dashboard, you can view playbook and task errors, average playbook run time, and execution by status for manual and automated tasks. You can also pivot to the XQL view for more detailed data analysis.

### Increase the timeout for AI prompt tasks

AI prompt tasks have a default execution timeout of 10 seconds. If an AI prompt task returns a **`504 Error`** with the status **`DEADLINE_EXCEEDED`**, it is likely due to the task requiring more time to process than the default setting allows. To resolve this, open the Task Details pane of the AI task and select the Advanced tab, then increase the Execution timeout (seconds) value based on the complexity of the prompt and the expected length of the LLM response. For example, for complex tasks such as generating a full vulnerability report, you many need to increase the timeout from the 10 second default to 120 seconds or higher.
