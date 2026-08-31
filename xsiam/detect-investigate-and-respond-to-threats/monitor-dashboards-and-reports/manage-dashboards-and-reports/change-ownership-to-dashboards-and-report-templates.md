---
description: >-
  Change Cortex XSIAM dashboard and report template ownership to maintain access
  and accountability.
---

# Change ownership to dashboards and report templates

Only administrators can change the ownership of a custom dashboard or report template.

{% hint style="info" %}
**Note:** For report templates, when ownership is transferred, any existing report schedules associated with the template are automatically removed. The new **Owner** must manually redefine the schedule to resume automated report generation.
{% endhint %}

{% stepper %}
{% step %}
**Open change owner**

Right-click the custom dashboard or template and select **Change owner**.
{% endstep %}

{% step %}
**Select a new owner**

Select the new owner from the list of users.
{% endstep %}

{% step %}
**Confirm the change**

For templates, review the warning regarding deleted schedules and click **Change**.
{% endstep %}
{% endstepper %}
