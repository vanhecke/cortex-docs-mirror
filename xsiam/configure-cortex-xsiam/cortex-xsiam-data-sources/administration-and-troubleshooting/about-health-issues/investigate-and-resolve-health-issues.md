---
description: >-
  Investigate and resolve ingestion, collection, correlation, and automation
  health issues in Cortex XSIAM.
---

# Investigate and resolve health issues

The following tasks explain how to investigate and resolve health issues. You can see health issues on the following pages:

* Go to Settings → Health Issues
* Go to Cases & Issues → Issues and change the table view to Health Domain.

### **Investigate data ingestion errors in Cortex XSIAM**

A data ingestion issue identifies disruption in the data ingestion pipeline. For example, a data source is not sending logs, or there is a significant drop in log collection compared to the calculated ingestion baseline.

1. Identify the error: Type = Ingestion.
2.  Right-click and select Investigate in XQL query.

    The Query Builder opens and runs a prefilled query to display related data ingestion metrics entries.
3.  Review the query results.

    The results provide context for the issue and the events leading up to it. For more information about data ingestion metrics and setting up correlation rules with your own data ingestion logic, see [Monitor data ingestion health](monitor-data-ingestion-health).
4.  Investigate data collector errors. Return to the Health Issues page, right-click the issue, and select Pivot to views → View collector details.

    Depending on the type of collector in error, the relevant data collector settings page opens, filtered by data collector.

### **Investigate collection errors in Cortex XSIAM**

A collection issue identifies connectivity disruption in your collection integrations, custom collectors, and Marketplace integrations.

1. Identify the error: Type = Collection.
2.  See the current status of the collector.

    Right-click and select Pivot to views → View collector details. Depending on the type of collector in error, the relevant data collector settings page opens, filtered by data collector.

    If the data collector is still in error, you can update the collector settings as required.
3.  Investigate the collector error status.

    Run a query on the `collection_auditing` dataset to see all the connectivity changes of the collector over time, the escalation or recovery of the connectivity status, and the error, warning, and informational messages related to status changes.

    This example searches for status changes for the "instance1" data collector integration:

    ```
    dataset = collection_auditing 
    |filter collector_type = "STRATA_IOT" and instance = "instance1"
    ```

    <br>

    For more information about troubleshooting collector errors and setting up correlation rules to trigger additional collection issues, see [Verify collector connectivity](../verify-collector-connectivity).

### **Investigate correlation errors in Cortex XSIAM**

A correlation issue identifies errors in your correlation rules.

1. Identify the error: Type = Correlation.
2.  Right-click and select Investigate Correlation Auditing.

    The Query Builder opens and runs a prefilled query to display related correlation execution records.
3.  Review the query results.

    Identify the correlation rule in error and take steps to resolve the error. For more information about how Cortex XSIAM identifies correlation rule errors, see [Monitor correlation rules](monitor-correlation-rules).

### **Investigate automation errors in Cortex XSIAM**

Automation issues identify potential misconfigurations in automations, enabling you to take a proactive approach to fixing misconfiguration issues before they affect system performance.

1. Identify the error: Type = Automation.
2. Click the automation health issue to view the details of the related case or component.
3. Based on the details of the automation health issue, review any related automations, such as playbooks and integrations, for possible misconfigurations.

<br>
