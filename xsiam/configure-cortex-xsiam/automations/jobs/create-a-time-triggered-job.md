---
description: Schedule a playbook to run at a specific time
---

# Create a time-triggered job

Time-triggered jobs run at predetermined times. You can schedule the job to run at a recurring time or one time at a specific date and time.

{% hint style="warning" %}
### Configure your playbook to close the investigation

A scheduled job automatically opens an internal investigation container to run its playbook. Because the platform allows for manual post-playbook analysis, finishing the playbook tasks does not automatically close this container. If left open, the overall job remains stuck in a Running status. To ensure a consistent UI status, you must add a task to close the investigation at the end of your playbook:

1. Navigate to **Investigation & Response** → **Automation** → **Playbook** and open the playbook in the editor.
2. In the **Task Library** on the left, search for closeInvestigation (this is an out-of-the-box system command) located under **Builtin Commands**.
3. Add the closeInvestigation task to your canvas and configure it as the final step on the successful execution path of your playbook.
{% endhint %}

1. Select **Investigation & Response** → **Automation** → **Jobs** → **New Job**.
2. Select **Time triggered**.
3.  If you want the job to repeat at regular intervals, select **Recurring** and select the desired interval.

    You can choose to run the job every X number of days, on specific days of the week, at a specific time and also choose a start date and an expiration date.

    You can configure the recurring job using a cron expression. To do so, after selecting the **Recurring** checkbox, click **Switch to Cron view** and enter the expression. For help defining the cron expression, click **Show cron examples** after switching to cron view.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To view a human-readable description of a cron schedule for an existing job, click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-d6f550520d22a98972bdf1be8edcdbff82082975%2F0d46ae791454ea7d03c60c4132363fd71fa07f01a5fa8a5d982972a170b121a5.png?alt=media" alt="settings-wheel.png"> and select <strong>Job Schedule</strong> from the available columns.</p></div>
4. If you do not want the job to repeat, select the **date and time** for the job to run.
5.  In the **BASIC INFORMATION**, section, add relevant time-triggered job parameters from the following:

    | Name        | Description                                                 |
    | ----------- | ----------------------------------------------------------- |
    | Name        | Enter a meaningful name for the job.                        |
    | Playbook    | Determine which playbook to run when this job is triggered. |
    | Description | Enter a meaningful description of the job.                  |
6.  In the **QUEUE HANDLING** section, select one of the following response options to use if the job is triggered while a previous run of the job is active:

    * Don’t trigger a new job run
    * Cancel the previous job run and trigger a new job run
    * Trigger a new job run and execute concurrently with the previous run

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>We recommend avoiding triggering a job while a previous run of the job is active by configuring the playbook a job triggers to close the investigation before running a new instance of the job.</p></div>
7. Ensure that the playbook assigned to this job includes the closeInvestigation built-in command as its final execution step. This action closes the underlying container workspace and enables the user interface to show the accurate completion status.
8. Select **Create new job**.
