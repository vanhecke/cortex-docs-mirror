# Enable the Analytics Engine and Identity Analytics

Cortex XSIAM - Analytics includes the following:

* **Cortex XSIAM Analytics Engine:** Analyzes your endpoint data to develop a baseline and raise Analytics and Analytics BIOC alerts when anomalies and malicious behaviors are detected.
* **Identity Analytics:** Allows the Cortex XSIAM Analytics engine to aggregate and display user profile details, activities, and alerts related to a user-based Analytics type alert and Analytics BIOC rule during an investigation.

{% hint style="warning" %}
### Prerequisite

**Analytics Engine**

To create a baseline for enabling analytics, Cortex XSIAM requires a minimum of one of the following data sets:

* EDR or Network logs from at least 30 endpoints over a minimum of 2 weeks
* Cloud audit logs over a minimum of 5 days

**Identity Analytics**

* Cortex XSIAM - Analytics must be activated.
* Cloud Identity Engine must be set up. For more information, see [Cloud Identity Engine](../set-up-cloud-identity-engine).
{% endhint %}

How to enable analytics

1. Select **Settings** → **Configurations** → **Cortex XSIAM - Analytics**.
2.  Click **Enable**. Creating a baseline can take up to three hours.

    Adding Windows DHCP logs can enhance the Analytics Engine. For more information, see Ingest Windows DHCP Logs with an XDR Collector Profile.
3. Activate **Identity Analytics** by turning on the toggle.
