---
description: >-
  Configure Active Directory Certificate Services (ADCS) auditing events for
  Cortex XSIAM data collection.
---

# Additional setup for Active Directory Certificate Services (ADCS) events

ADCS events with IDs 4880, 4881, 4886, 4887, 4896, 4898, 4899, 4900 require additional setup.

{% hint style="info" %}
### Note

Enabling auditing for Active Directory Certificate Services (ADCS) restarts (events 4880 and 4881) can significantly slow down the service if you have a large database. To prevent delays:

* Clean up the database: Remove any unnecessary entries to reduce its size.
* Skip this audit: If restart speed is critical, consider not enabling auditing for ADCS starts and stops (event IDs 4880 and 4881).
{% endhint %}
