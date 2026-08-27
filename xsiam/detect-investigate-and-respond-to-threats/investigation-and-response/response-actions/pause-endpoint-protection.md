---
description: >-
  Temporarily pause Cortex XSIAM endpoint protection for approved
  troubleshooting or maintenance tasks.
---

# Pause endpoint protection

As of agent 7.7 and above, you can pause the agent protection capabilities on one or more endpoints while maintaining connectivity with Cortex XSIAM. By only pausing the protection and retaining connectivity, the agent will run with all the profiles disabled, but continue to send data and take actions from the server. When you are ready, you can resume the endpoint protection.

{% hint style="info" %}
Pausing your endpoint protection modules leaves your machines exposed to risks.
{% endhint %}

### How to pause endpoint protection modules

1. Go to **Inventory→ Endpoints** → **All Endpoints**.
2. In the **All Endpoints** page, select the endpoints on which you want to pause protection, right-click and select Endpoint Control → **Pause Endpoint Protection**.
3.  Verify the endpoints, add an optional comment that appears in the Management Audit log, and **Pause** the protection.

    Paused endpoints display a pause icon in the **Endpoint Name** field, and one of the following the action statuses in **Manual Protection Pause** field:

    * Protection Active
    * Pending Pause
    * Protection Paused
    * Pending Activation
4.  When you are ready to resume protection, select the paused endpoints, right-click and select Endpoint Control → **Resume Endpoint Protection** and **Resume** protection on the listed endpoints.

    The **All Endpoint** table fields are updated accordingly.
5.  Track your pause and resume endpoint protection actions.

    Go to Investigation & Response → Response → **Action Center** and locate **Action Type** **Pause Endpoint Protection** or **Resume Endpoint Protection**.
