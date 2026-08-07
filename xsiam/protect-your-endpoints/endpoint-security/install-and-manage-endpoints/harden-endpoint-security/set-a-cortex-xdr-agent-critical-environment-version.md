# Set a Cortex XDR agent Critical Environment version

After you install the Cortex XDR agent and the agent registers with Cortex XSIAM, you can set endpoints to run with a Cortex XDR agent Critical Environment (CE) version.

CE versions are designed for sensitive and highly regulated environments. These versions receive full content update coverage and contain the same feature set as the standard line it is based on. Please note, that some bug fixes, introducing higher stability risk, may not be incorporated into the maintenance releases of these lines. Support is provided for CE versions for 24 months, while support for standard versions is provided for 9 months.

To ensure the stability of the line, CE versions maintenance release cadence is longer than in the standard line, we recommend that deployment is adjusted accordingly.

Setting an endpoint with a CE agent version requires you to define your agent configurations which then allows you to do the following:

* Create a CE agent installation package
* Define the upgrade and auto-upgrade in the Agent Settings Profile

{% stepper %}
{% step %}
### Define your agent configuration.

1. Navigate to Settings → Configurations → General → Agent Configurations. Scroll down to Critical Environment Versions.
2. Click Enable Critical Environment Versions to be Created and Installed in the Tenant.
{% endstep %}

{% step %}
### Track endpoints with CE Agent versions.

Navigate to Inventory → Endpoints → All Endpoints. In the table, locate the Version Type field to view whether the endpoint is defined as a Standard or Critical Environment agent.
{% endstep %}
{% endstepper %}
