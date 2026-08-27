---
description: Investigate SHA256 file and process hashes in Cortex XSIAM.
---

# Investigate a file and process hash

Drilldown on a file or process hash on the Hash View in Cortex XSIAM. On this view you can investigate and take actions on SHA256 hash processes and files, and see information about a specific SHA256 hash over a defined 24-hour or 7-day time frame. In addition, you can drill down on each of the process executions, file operations, cases, actions, and threat intelligence reports relating to the hash.

### How to investigate a file or process hash

1.  Open the Hash View.

    Identify the file or process hash that you want to investigate and select Open Hash View.
2. In the left panel, review the overview of the hash.
   1. Review the signature of the hash, if available.
   2.  Identify the WildFire verdict.

       The color of the hash value is color-coded to indicate the WildFire report verdict:
   3. Add an Alias or Comment to the hash value.
   4.  Review threat intelligence for the hash.

       Depending on the threat intelligence sources that are integrated with Cortex XSIAM, the following threat intelligence might be available:

       *   Virus Total score and report.

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Requires a license key. Go to <strong>Settings → Configurations → Integrations → Threat Intelligence</strong>.</p></div>
       * IOC Rule, if applicable, including the IOC Severity, Number of hits, and Source according to the color-coded values:
       * WildFire analysis report.
   5. Review if the hash has been added to:
      * Allow List or Block List.
      * Quarantined, select the number of endpoints to open the Quarantine Details view.
   6. Review the recent open cases that contain the hash as part of the case's Key Artifacts according to the Last Updated timestamp. To dive deeper into specific cases, select the Case ID.

<details>

<summary>WildFire color key</summary>

* Blue—Benign
* Yellow—Grayware
* Red—Malware
* Light gray—Unknown verdict
* Dark gray—The verdict is inconclusive

</details>

3. In the right hand view, use the filter criteria to refine the scope of the IP address information that you want to visualize.

<details>

<summary>Filter criteria</summary>

<table><thead><tr><th width="140">Event Type</th><th>Main set of values that you want to display. The values depend on the selected type of process or file.</th></tr></thead><tbody><tr><td>Primary</td><td>Set of values that you want to apply as the primary set of aggregations. Values depend on the selected Event Type.</td></tr><tr><td>Secondary</td><td>Set of values that you want to apply as the secondary set of aggregations.</td></tr><tr><td>Showing</td><td>Number of Primary and Secondary aggregated values to display.</td></tr><tr><td>Timeframe</td><td>Time period over which to display your defined set of values.</td></tr></tbody></table>

</details>

4.  Review the selected data.

    To view the most recent processes executed by the hash, select Recent Process Executions. To run a query on the hash, select Search all Process Executions.
5. (Optional) Perform actions on the hash.
