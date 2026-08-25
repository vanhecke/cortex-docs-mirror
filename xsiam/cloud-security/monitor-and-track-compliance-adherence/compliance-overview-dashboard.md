---
description: >-
  Monitor organization-wide Cortex XSIAM compliance scores, standards, failed
  controls, and asset group performance.
---

# Compliance Overview Dashboard

The **Compliance Overview Dashboard** is an out-of-the-box dashboard that presents a centralized view of your organization's compliance performance against industry standards and your own internal security frameworks.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FQlELXdRxQXuLSW4wi1dZ%2Fimage.png?alt=media&#x26;token=d8994fb7-7759-4978-8a0e-5a6aa296a273" alt=""><figcaption></figcaption></figure>

The Compliance Overview Dashboard provides an immediate and clear visual representation of the organization’s overall compliance posture. By integrating a comparative view, the dashboard allows you to evaluate performance across the monitored environment against assessed compliance standards.

### How to access

1. Navigate to **Dashboards & Reports** → **Dashboard.**
2. From the dashboard header, a drop-down menu lists all available predefined and custom dashboards. Find the **Compliance Overview** dashboard on that list and click on it.

### Dashboard filters

The global filters enable you to refine dashboard data for more granular analysis. You can filter the view using six filters:

* **Standard:** Select specific frameworks such as CIS, NIST, or PCI DSS.
* **Category:** Narrow results by high-level groupings within a chosen standard.
* **Control:** Drill down into specific compliance controls.
* **Assessment:** Isolate results from one or more specific compliance assessment runs.

Click **Run** to apply the selected filters.

Click **Reset Filters** to clear all filters.

### Refreshing the dashboard

The **Last updated** date on top of the page provides the time stamp for when the dashboard was last updated. The widgets and filters are refreshed every 10 minutes. You can refresh the content of each widget manually by clicking on **Refresh**.

{% hint style="info" %}
**NOTE**

If you just created an assessment profile, it may take up to 10 minutes for it to appear in the Assessment filter. As a workaround, you can refresh the URL in the browser.
{% endhint %}

### Dashboard widgets

The dashboard includes the following information:

| **Dashboard widget**              | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Compliance Overview**           | <p>These high-level compliance metrics provide an executive summary of the environment’s health:</p><ul><li><strong>Compliance Score:</strong> An aggregated percentage representing overall adherence across all active standards and assets. For more information, see <a href="../view-and-manage-compliance-assessments-and-reports#compliance-score">Compliance score</a>.</li><li><strong>Assets Assessed:</strong> The total number of unique cloud resources currently being evaluated against compliance rules.</li><li><strong>Total Assets:</strong> The complete inventory of discovered assets, including those not currently included in a compliance assessment profile.</li></ul> |
| **Compliance Standards Overview** | Displays compliance progress (“Compliance Score”) against specific standards. This widget displays up to 200 standards sorted by compliance score in descending order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **Failed Controls by Severity**   | <p>Displays a chart and legend categorizing all compliance failures to assist in prioritization:</p><ul><li><strong>Critical:</strong> Immediate risks that require urgent remediation.</li><li><strong>High:</strong> Significant security gaps.</li><li><strong>Medium:</strong> Moderate deviations from best practices.</li><li><strong>Low:</strong> Minor deviations from best practices.</li><li><strong>Informational:</strong> Observations that do not necessarily impact the score but provide environmental context.</li></ul><p>You can toggle between two views.</p>                                                                                                                |
| **Most Failed Controls**          | Identifies 10 specific security controls causing the highest volume of failures. For each control, it shows which standards it belongs to and provides the raw count of resources failing that specific check.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Most Compliant Asset Groups**   | Lists 10 asset groups with the highest compliance scores, sorted in descending order. Shows compliance score of asset groups, in descending order. This section highlights high-performing segments of the environment. This allows administrators to validate that security policies are effectively applied in production environments.                                                                                                                                                                                                                                                                                                                                                         |
| **Least Compliant Asset Groups**  | Lists 10 asset groups with the lowest compliance scores, sorted by compliance score in ascending order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
