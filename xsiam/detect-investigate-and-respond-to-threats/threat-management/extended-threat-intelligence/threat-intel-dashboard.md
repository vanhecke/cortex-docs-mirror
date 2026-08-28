---
description: >-
  Use the Cortex XSIAM Threat Intel Dashboard to monitor intelligence
  distribution, ingestion health, and emerging threats.
---

# Threat Intel Dashboard

The **Threat Intel Dashboard** visualizes threat intelligence data, such as threat objects and indicators, within your environment to help you understand data distribution and identify trends.

You can use the dashboard as provided or clone and modify it to suit your needs.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FEpQIzeotW51HYMVhvRXz%2Funknown.png?alt=media&#x26;token=f880be13-5ea6-4745-8e46-5b868ccbf045" alt="This screenshot from Cortex UI shows the Threat Intel Dashboard." height="423" width="624"><figcaption></figcaption></figure>

## Accessing the dashboard

To access the dashboard, go to **Threat Management → Threat Intelligence → Dashboard**.

Alternatively, you can access it from **Dashboards & Reports → Dashboard**. From the dashboard header, a menu lists all available predefined and custom dashboards. Find the **Threat Intel Dashboard** dashboard on that list and select it.

If you position the cursor over a specific dashboard widget, you can access the related XQL query by selecting the XQL link in the top-right corner of the widget:

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FqhAsdmrpK2GSifCHj25P%2Funknown.png?alt=media&#x26;token=9e4efd68-1fef-4829-8fac-79ca60e850c0" alt="This screenshot from Cortex UI shows how to view the XQL source behind a widget in the Threat Intel Dashboard." height="240" width="446"><figcaption></figcaption></figure>

## Dashboard content

The Threat Intelligence Dashboard serves as a comprehensive overview of Unit 42 threat intelligence data, helping you understand data distribution and identify trends.

The dashboard starts with a high-level overview of ingestion health and data distribution to ensure all streams from Unit 42 remain active.

As you move down, the data becomes increasingly granular. The second row breaks down top threat actors and malware families by specific IOC counts, while the third row expands the scope to provide a holistic view of indicators across the entire environment.

These categories are separated because file-based data typically arrives in much larger volumes than network traffic data, and each represents a distinct technical domain—one focused on file processes and the other on network communication.

**Related links**

For general information about dashboards, see [Monitor dashboards and reports](../../monitor-dashboards-and-reports).

<br>
