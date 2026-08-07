# Manage quarantined files

When the agent detects malware on a Windows endpoint, you can take additional precautions to quarantine the file. When the agent quarantines malware, it moves the file from the location on a local or removable drive to a local quarantine folder (`%PROGRAMDATA%\Cyvera\Quarantine`) where it isolates the file. This prevents the file from attempting to run again from the same path or causing any harm to your endpoints.

To evaluate whether an executable file is considered malicious, the agent calculates a verdict using information from the following sources in order of priority:

* Hash exception policy
* WildFire threat intelligence
* Local analysis

### How to quarantine a file

You can quarantine a file in the following ways:

* Enable the agent to automatically quarantine malicious executables by configuring quarantine settings in a Malware prevention profile. For more information, see [Set up malware prevention profiles](https://app.gitbook.com/s/mxWuY3s7AUvWfzCV9p1A/endpoint-security/install-and-manage-endpoints/set-up-endpoint-protection/set-up-endpoint-profiles-and-exception-rules/set-up-malware-prevention-profiles).
* Right-click a specific file from the causality view and select **Quarantine**.

### View and manage quarantined files

{% hint style="info" %}
Requires the Cortex XSIAM Premium, Enterprise, or any other XSIAM license with the Enterprise Runtime Security or the Cloud Runtime Security add-on.
{% endhint %}

1.  To view the quarantined files in your network, go to **Investigation & Response → Response → Action Center →** **File Quarantine**.

    Toggle between the **Detailed** and **Aggregated By SHA256** tabs to see information on your quarantined files.
2.  Review details about quarantined files.

    In the **Detailed** view, filter and review the **Endpoint Name**, **Domain**, **File Path**, **Quarantine Source**, and **Quarantine Date** of all the quarantined files. You can take the following actions:

    *   **Reinstate a quarantined file:** Right-click one or more rows and select **Restore all files by SHA256**.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>This will restore all files with the same hash on all of your endpoints.</p></div>
    * **Review the quarantined file inspection results on VirusTotal:** Right-click the **Hash** field and select **Open in VirusTotal**.
    * **Drill down on the hash value:** Right-click the **Hash** field and select **Open Hash View**. You can see each of the process executions, file operations, cases, actions, and threat intelligence reports relating to the hash value.
    * **Search for where the hash value appears in Cortex XSIAM:** Right-click the **Hash** field and select **Open in Quick Launcher**.
    * **Export to file:** Click the icon on the top right corner to download a detailed list of the quarantined hashes in a TSV format.
3. In the **Aggregated by SHA256** view, filter and review the **Hash**, **File Name**, **File Path**, and **Scope** of all the quarantined files. You can take the following actions:
   * **Open the Quarantine Details page:** Right-click a row and select **Additional Data** to open the page detailing the **Endpoint Name**, **Domain**, **File Path**, **Quarantine Source**, and **Quarantine Date** of a specific file hash.
   * **Reinstate a file hash:** Right-click and select **Restore**.
   * **Permanently delete quarantined files on the endpoint:** Right-click and select **Delete all files by SHA256**.
