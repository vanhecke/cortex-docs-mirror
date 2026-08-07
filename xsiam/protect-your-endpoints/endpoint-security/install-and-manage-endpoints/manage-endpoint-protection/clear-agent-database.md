# Clear agent database

Learn how to clear the Cortex XDR agent database.

If one or more Cortex XDR agents are having issues, you can attempt a reset by clearing the Cortex XDR agent state of one or more endpoints.

{% hint style="info" %}
**Note:**

Clearing the agent database is supported on all platforms with Cortex XDR agent version 7.9 or later, and is available only when using the debugging mode.
{% endhint %}

Clearing the agent database is available only when using the debugging mode, and can be tracked in the Action Center.

{% stepper %}
{% step %}
#### Clear Agent Database.

* Navigate to **Inventory → Endpoints → All Endpoints** and select one or more endpoints for which you want to clear the database.
* In Windows, press ALT and right-click, or in macOS press Option and right-click, to open the context menu in debugging mode.
* Navigate to **Endpoint Control → Clear Agent Database**.
{% endstep %}

{% step %}
#### Track progress of the Clear Database action.

* Navigate to **Investigation & Response → Response → Action Center**.
* In the All Actions table, filter the Action Type field according to Agent Database Cleanup.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
**Note:**

You can only right-click to cancel the clear agent database for actions with a pending status.
{% endhint %}
