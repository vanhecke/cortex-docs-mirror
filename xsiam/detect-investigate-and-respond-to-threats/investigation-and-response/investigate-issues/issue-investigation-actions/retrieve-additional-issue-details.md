---
description: >-
  Retrieve Cortex XSIAM issue data, related files, and packet captures for
  analysis.
---

# Retrieve additional issue details

To help you with issue analysis, Cortex XSIAM can provide related files and memory content analysis.

1. From the **Issues** page, locate the issue for which you want to retrieve information.
2. Right-click anywhere in the issue, and select one of the following options:
   * **Retrieve Additional Data:** Cortex XSIAM can provide related files and additional analysis of the memory contents when an exploit protection module raises an issue.
     * Select **Retrieve issue data and analyze** to retrieve issue data consisting of the memory contents at the time the issue was raised. You can also enable Cortex XSIAM to automatically retrieve issue data for every relevant issue. After Cortex XSIAM receives the data and performs the analysis, it issues a verdict for the issue. You can monitor the retrieval and analysis progress from the **Action Center** (pivot to view **Additional data**). When the analysis is complete, it displays the verdict in the **Advanced Analysis** field.
     * **Retrieve related files:** To further examine files that are involved in an issue, you can request the agent send them to the Cortex XSIAM tenant. If multiple files are involved, the tenant supports up to 20 files and 200MB in total size. The agent collects all requested files into one archive and includes a log in JSON format containing additional status information. When the files are successfully uploaded, you can download them from the **Action Center** for up to one week.
     *   **Pivot to views** → **View in source system**: For issues ingested from third-party vendors, this option pivots to the issue in the third-party system.

         To enable this feature, ensure that Cortex XSIAM has a correlation rule that contains the **External URL** field. For more information, refer to [Create a correlation rule](../../../threat-management/detection-rules/what-are-detection-rules/whats-a-correlation-rule/create-a-correlation-rule).
   * (For **PAN NGFW** source type issues) **Download triggering packet:** Download the session PCAP containing the first 100 bytes of the triggering packet directly from Cortex XSIAM. To access the PCAP, you can download the file from the Issues table, Cases, or Causality view.
3. Navigate to Investigation & Response+Response → **Action Center** to view the retrieval status.
4.  Download the retrieved files locally.

    In the **Action Center**, wait for the data retrieval action to complete successfully. Then, right-click the action row and select **Additional Data**. From the **Detailed Results** view, right-click the row and select **Download Files**. A ZIP folder with the retrieved data is downloaded locally.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Tip</h4><p>If you require assistance from Palo Alto Networks support to investigate the issue, make sure to provide the downloaded ZIP file.</p></div>
