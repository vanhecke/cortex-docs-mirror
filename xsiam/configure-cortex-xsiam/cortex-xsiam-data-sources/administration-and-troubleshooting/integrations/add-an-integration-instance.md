---
description: Add and configure an integration instance in Cortex XSIAM.
---

# Add an integration instance

To use a downloaded integration, you must configure an integration instance.

Before you begin:

* Content packs containing integrations are downloaded when you adopt playbooks and configure playbook tasks. The content pack must be downloaded before you can configure an integration instance.
* Consider whether you want to add credentials, which enable you to save login information without exposing usernames, passwords, certificates, and SSH keys. For more information, see [Manage credentials](manage-credentials).
* Although you can view integration documentation when adding an instance, [https://xsoar.pan.dev/](https://xsoar.pan.dev/docs/reference/index) has more detailed information about integrations, including commands, outputs, and recommended permissions.

{% stepper %}
{% step %}
### Find the integration

Navigate to **Settings** → **Data Sources & Integrations**. Search for the integration.
{% endstep %}

{% step %}
### Add an instance

Select the integration and click **Add Instance**.
{% endstep %}

{% step %}
### Configure parameters

Add the required parameters.
{% endstep %}

{% step %}
### Test the connection

Optional: Click **Test** to verify the integration instance works correctly.
{% endstep %}

{% step %}
### Save the instance

Click **Save & Exit**.

You can expand the integration to view instance details. You can also enable, disable, or copy the instance.

If an error occurs, see [Troubleshoot integrations](troubleshoot-integrations).
{% endstep %}

{% step %}
### Choose when to use the instance

By default, the instance runs whenever the integration is called. Change **Always** to **On Demand** to use it only with the `using` argument in a playbook or CLI.

For example, use an on-demand instance for manual testing.
{% endstep %}

{% step %}
### Configure command access

Optional: See [Configure integration permissions](configure-integration-permissions) to manage access to specific commands.
{% endstep %}
{% endstepper %}
