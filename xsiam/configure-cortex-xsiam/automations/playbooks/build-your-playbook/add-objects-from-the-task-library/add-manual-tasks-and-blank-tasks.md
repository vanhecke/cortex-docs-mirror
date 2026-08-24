---
description: Add manual and blank tasks to Cortex XSIAM playbooks.
---

# Add manual tasks and blank tasks

Using the Task Library, add manual or blank tasks to a playbook.

Cortex XSIAM supports task types for different playbook actions.

### Add a manual task

**Manual Tasks** lists playbooks in your Org repository and their manual tasks. These tasks do not run scripts and may require manual input.

By default, playbooks are sorted by their latest update. You can also sort playbooks alphabetically.

{% stepper %}
{% step %}
In the **Task Library** pane, select **Manual Tasks**.
{% endstep %}

{% step %}
Select a playbook to view its tasks.
{% endstep %}

{% step %}
Drag the required task onto the playbook editor.
{% endstep %}

{% step %}
Connect the added task by dragging a wire to it.
{% endstep %}

{% step %}
Save the playbook.
{% endstep %}
{% endstepper %}

A user icon identifies tasks that require manual input. Change the task settings to automate the task.

### Add a blank task

A **Blank Task** lets you create a custom task from scratch.

{% stepper %}
{% step %}
In the **Task Library** pane, select **Blank Task**.
{% endstep %}

{% step %}
In the **Task Details** pane, select a **Task Type**.

* **Standard task** — Confirm information or escalate a case.
* **Conditional task** — Validate values or parameters and direct the workflow.
* **Data Collection task** — Collect information from users in your organization.
* **Section Header** — Group related tasks and organize the playbook flow.
{% endstep %}

{% step %}
Enter a meaningful name in **Task Name**.
{% endstep %}

{% step %}
Configure settings for the selected task type.

See [Add objects from the Task Library]() for task type details.
{% endstep %}

{% step %}
Select **Save**.

The task is added to the playbook editor.
{% endstep %}

{% step %}
Connect tasks in their logical order by dragging a wire between them.
{% endstep %}

{% step %}
Save the playbook.
{% endstep %}
{% endstepper %}
