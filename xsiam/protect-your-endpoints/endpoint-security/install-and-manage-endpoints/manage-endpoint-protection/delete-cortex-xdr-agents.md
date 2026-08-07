# Delete Cortex XDR agents

If you have an endpoint that you no longer want to track through Cortex XSIAM, for example, if the endpoint disconnected from Cortex XSIAM, or an endpoint where the Cortex XDR agent was uninstalled, you can delete the endpoint from the Cortex XSIAM tenant views.

Deleting an endpoint triggers the following lifespan flow:

* The endpoint status changes to **Deleted** , and the license returns immediately to the license pool. After a retention period of 90 days, the agent is deleted from the database and is displayed in Cortex XSIAM as Endpoint Name - `N/A (Deleted)`.
* Data associated with the deleted endpoint is displayed in the Action Center tables and in the Causality View for the standard 90-day retention period.
* Alerts that already include the endpoint data at the time of alert creation are not affected.

Additionally, Cortex XSIAM automatically deletes agents after a long period of inactivity.

* **Standard agents** are deleted after 180 days of inactivity. Where day one is the first 24 hours of continuous inactivity.
* **VDI and TS agents** are deleted after 6 hours of inactivity.

{% hint style="info" %}
**Note:**

To reinstate an endpoint, you have to uninstall and reinstall the agent.
{% endhint %}

The following workflow describes how to delete the Cortex XDR agent from one or more Windows, Mac, or Linux endpoints.

1. Select **Inventory → Endpoints → All Endpoints**.
2. Right-click the endpoint you want to remove.

You can also select multiple endpoints if you want to perform a bulk delete.

3. Select **Endpoint Control → Delete Endpoint**.
