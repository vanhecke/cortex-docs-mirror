# Jobs permissions

Configure access to automation jobs. Jobs are scheduled playbook tasks that run at predefined intervals or in response to feed changes.

By default, the **Jobs** permission is set to **None**. While you can enable the Jobs permission itself, you will not be able to select playbooks to run within the job unless you have at least Viewer access to those playbooks. Additionally, viewing the results of a job within a case requires access to the Cases & Issues component.

| Permission | Description                                                                                                            | Roles Example                                                                                |
| ---------- | ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| View/Edit  | Users can create, edit, enable/disable, and delete jobs. They can also manually trigger a job to **Run now**.          | SOC Manager / Security Engineer: Needs full control over scheduling and operational tasks.   |
| View       | Users can view the list of all scheduled jobs, their status (Running, Error, etc.), and their next scheduled run time. | Compliance Auditor: Needs to verify that automated cleanup or reporting tasks are scheduled. |
| None       | Cannot access the Jobs page or view any job configurations.                                                            | Standard User: Does not require access to backend automation scheduling.                     |

### Required and recommended permissions

To work with jobs, an administrator must configure your user role with specific RBAC permissions.

<table><thead><tr><th width="238">Component</th><th>Permission Level</th><th>Reason</th></tr></thead><tbody><tr><td><strong>Scripts</strong> (under <strong>Investigation &#x26; Response</strong> > <strong>Automations</strong>)</td><td>Enabled</td><td>Required to view and manage the underlying scripts used in automation workflows.</td></tr><tr><td><strong>Playbooks</strong> (under <strong>Investigation &#x26; Response</strong> > <strong>Automations</strong>)</td><td>Enabled</td><td>Required to select and view the playbook logic that a job will execute.</td></tr><tr><td><strong>Jobs</strong> (under <strong>Investigation &#x26; Response</strong> > <strong>Automations</strong>)</td><td>View or View/Edit</td><td>Enables access to the Jobs page to monitor or manage scheduled tasks.</td></tr><tr><td><strong>Cases and Issues</strong> (under <strong>Cases &#x26; Issues</strong>)</td><td>View or View/Edit</td><td>Required to view the results (War Room/Work Plan) of jobs executed within an investigation container.</td></tr></tbody></table>

### Important considerations

* **Visibility**: For all users with View or Edit permissions, all Jobs are listed regardless of the user's object-level access to the specific Playbooks used in those jobs.
* **System execution**: Playbooks triggered by jobs run as "system". They are governed by the permissions of the involved integrations rather than the access context of the user who created the job.
* **Execution results**: To view the War Room or Work Plan for an investigation opened by a job, the user must have the **Cases & Issues** permission set to **View** or **View/Edit** (which in turn requires **Playbooks** and **Scripts** to be enabled).
