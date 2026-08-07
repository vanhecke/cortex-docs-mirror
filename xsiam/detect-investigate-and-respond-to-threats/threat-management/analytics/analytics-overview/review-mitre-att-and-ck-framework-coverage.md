# Review MITRE ATT\&CK framework coverage

You can see a comprehensive overview of the Cortex XSIAM content and capabilities in context with the MITRE ATT\&CK framework on the MITRE ATT\&CK Framework Coverage dashboard. Access the dashboard from the drop-down menu in the dashboard header.

On this dashboard you can see a breakdown of the protection modules and detection rules in place for each MITRE tactic and technique. You can use the dashboard to review the elements that affect your coverage, and identify coverage gaps in your framework.

You can see the following information:

* **Number of detection rules per tactic:** Review the detection rules that are available for each MITRE tactic.
* **MITRE ATT\&CK framework coverage:** Review the MITRE matrix detailing the available coverage for each tactic and technique. By default, covered methods are displayed. Click on a tactic or technique for details about the available prevention and detection methods. Note that the Protection numbers represent modules, which are a grouping of several protections.
*   **Contributing data source types:** Review the connectivity status of the data sources that are contributing to a specific data source type on your system.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When a contributing data source type is active, it does not imply that all the rules and detectors associated with the data source type are active. Rule applicability is dependent on the data source's context and configuration. To enable an active status, data source types require the following setup:</p><ul><li><strong>Endpoint</strong>: Installed Cortex XDR agent.</li><li><strong>Network</strong>: A contributing network device that is configured to ingest logs as Cortex XSIAM network connection stories.</li><li><strong>Cloud</strong>: A data source that is contributing the required cloud related information.</li><li><strong>Identity</strong>: An identity application that is supported in IA (Identity Analytics) and the ITM (Identity Threat Module).</li></ul></div>

In addition, if you are working with reports, you can use the **MITRE Coverage Report** widget, which summarizes coverage for each tactic.

<br>
