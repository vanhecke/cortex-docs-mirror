---
description: Trigger a playbook when a feed changes
---

# Create a job triggered by a delta in a feed

Jobs triggered by a delta in a feed (event triggered jobs) run when a feed completes an operation and there is a change in the content. For the job to trigger, there must be a delta between the incoming feed and the previous one. You can define a job to trigger a playbook when the specified feed or feeds finish a fetch operation that includes a modification to the feed. The modification can be a new indicator, a modified indicator, or a removed indicator. For example, you may want to update your firewall every time a URL is added, modified, or removed from the Office 365 feed. You can configure a job that triggers the firewall update playbook to run whenever a modification is made to the feed.

{% hint style="info" %}
A job triggered by a delta in a feed runs only if there is a change in the feed, and does not run on a feed’s initial fetch. For the initial fetch, you can run the playbook manually and then set up an event triggered job for subsequent fetches.

If you want to trigger a job after a feed completes a fetch operation and the feed does not change frequently, you can select the **Reset last seen** option in the feed integration instance. The next time the feed fetches indicators, it will process them as new indicators in the system.
{% endhint %}

{% hint style="warning" %}
Configure your playbook to close the investigation.

A scheduled job automatically opens an internal investigation container to run its playbook. Because the platform allows for manual post-playbook analysis, finishing the playbook tasks does not automatically close this container. If left open, the overall job remains stuck in a Running status. To ensure a consistent UI status, you must add a task to close the investigation at the end of your playbook:

1. Navigate to Investigation & Response → Automation → Playbook and open the playbook in the editor.
2. In the Task Library on the left, search for closeInvestigation (this is an out-of-the-box system command) located under Builtin Commands.
3. Add the closeInvestigation task to your canvas and configure it as the final step on the successful execution path of your playbook.
{% endhint %}

1. Select **Investigation & Response** → **Automation** → **Jobs** → **New Job**.
2. Select **Triggered by delta in feed**.
3. In the **Trigger** section, select one of the following:
   * **Any feed**: The playbook runs when a modification is made to any feed.
   * **Specific feeds**: Select the feed instances that will trigger the playbook to run when a modification is made to them.
4. In the **BASIC INFORMATION** section:
   * Add a meaningful name for the job.
   * Select the playbook you want to run when the conditions for the job are met.
5. **Create a new job**.
