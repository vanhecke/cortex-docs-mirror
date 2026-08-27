---
description: >-
  Analyze Cortex XSIAM forensic evidence through issues, timelines, and key
  assets.
---

# Analysis and documentation

### Analysis and documentation

Forensic investigations include additional data for analysis and documentation purposes.

* Issues
* Forensics Timeline
* Key Assets & Artifacts

#### Review Issues

The issues table displays all the collections within the investigation that has identified suspicious or malicious activity within the forensics data sets.

Refer to [Overview of the Issues page](../investigate-issues/overview-of-the-issues-page) for descriptions of the table fields.

The following actions are available for a selected alert.

* Change status
* Change severity
* Investigate causality chain
* Run playbook
* Manage alerts

#### Investigation timeline

The Timeline page enables you to view the list of forensic artifacts that were tagged. The tags display details of the forensic data collected from the endpoints.

The **Timeline** table displays the following fields:

<table><thead><tr><th width="210">Field</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Name of the host machine.</td></tr><tr><td>Timestamp</td><td>Timestamp associated with the artifact.</td></tr><tr><td>Type</td><td>Forensic artifact of which a tag was added.</td></tr><tr><td>Description</td><td>Name of the timestamp field.</td></tr><tr><td>Tags</td><td><p>There are three default tags to choose from.</p><ul><li>legitimate</li><li>malicious</li><li>suspicious</li></ul><p>You can also create your own tags.</p></td></tr><tr><td>User</td><td>User account associated with the forensic artifact.</td></tr><tr><td>Data</td><td>Data summary for the tagged item.</td></tr><tr><td>Mitre Att&#x26;ck Tactic</td><td>Displays the type of MITRE ATT&#x26;CK tactic of the tagged item.</td></tr><tr><td>Mitre Att&#x26;ck Technique</td><td>Displays the type of MITRE ATT&#x26;CK technique of the tagged item.</td></tr><tr><td>Notes</td><td>Displays notes entered by the user.</td></tr></tbody></table>

1.  **Edit a timeline entry**

    You can edit a tag of an artifact in the **Timeline** table.

    1. Locate the relevant item to update the tag.
    2. Right-click and select **Edit timeline entry**.
    3. In **Edit timeline entry**, update the information as required and then click **Save** to update the changes.
2.  **Clear a timeline entry**

    You can remove a tag from the artifact in the **Timeline** table.

    1. Locate the relevant item to remove the tag.
    2. Right-click and select **Clear timeline entry**. The tag is removed from the artifact and the row is removed from the **Timeline** table.

#### Key assets & artifacts

Key assets & artifacts are automatically created based on the tagged data from the investigation timeline of the investigation and are divided among the categories:

* **Data Access**: Displays all the items that have been tagged in the File Access tables.

The following table for **Endpoints** displays the endpoints that have at least one or more items tagged:

<table><thead><tr><th width="178">Field</th><th>Description</th></tr></thead><tbody><tr><td>Endpoint Name</td><td>Name of the endpoint.</td></tr><tr><td>Endpoint Type</td><td><p>Displays the endpoint type:</p><ul><li>Mobile</li><li>Server</li><li>Workstation</li><li>Kubernetes Node</li></ul></td></tr><tr><td>Endpoint Status</td><td><p>Displays the status of the endpoint:</p><ul><li>Connected</li><li>Connected Lost</li><li>Deleted</li><li>Disconnected</li><li>Uninstalled</li><li>VDI Pending Login</li><li>Forensics Offline</li><li>Partial Registration</li></ul></td></tr><tr><td>Earliest Activity</td><td>Timestamp of the earliest tagged item in the incident timeline for the endpoint.</td></tr><tr><td>Latest Activity</td><td>Timestamp of the last tagged item in the incident timeline for the endpoint.</td></tr><tr><td>IP Address</td><td>List of associated IP addresses.</td></tr><tr><td>IPv6 Address</td><td>List of associated IPv6 addresses.</td></tr><tr><td>First Seen</td><td>Timestamp of first seen.</td></tr><tr><td>Last Seen</td><td>Timestamp of last seen.</td></tr><tr><td>Endpoint Isolated</td><td><p>Displays the status of endpoint isolation:</p><ul><li>Pending Isolation Cancellation</li><li>Pending Isolation</li><li>Isolated</li><li>Not Isolated</li></ul></td></tr><tr><td>Isolation Date</td><td>Isolation date of the endpoint.</td></tr></tbody></table>

The following table for **Malware** shows all the items that have been tagged in the Process Execution or Persistence tables.

<table><thead><tr><th width="167">Field</th><th>Description</th></tr></thead><tbody><tr><td>File Name</td><td>Name of the artifact collected from the endpoint.</td></tr><tr><td>Path</td><td>Executable path.</td></tr><tr><td>Tags</td><td>Assigned tags to the artifact.</td></tr><tr><td>SHA256</td><td>SHA256 value of the executable file.</td></tr><tr><td>Verdicts</td><td>WildFire verdicts.</td></tr><tr><td>User</td><td>User name of the person who ran the process.</td></tr><tr><td>Mitre ATT&#x26;CK Tactic</td><td>Tactic selected during tagging.</td></tr><tr><td>Mitre ATT&#x26;CK Technique</td><td>Technique selected during tagging.</td></tr><tr><td>Platform</td><td><p>Operating system of the endpoint:</p><ul><li>Windows</li><li>macOS</li><li>Linux</li><li>Android</li></ul></td></tr><tr><td>Created</td><td>Creation timestamp of the file accessed.</td></tr><tr><td>Accessed</td><td>Accessed timestamp of the file accessed.</td></tr><tr><td>Modified</td><td>Modified timestamp of the file accessed.</td></tr></tbody></table>

The following table for **Users** displays any artifact data with a non-null user field that has been tagged.

<table><thead><tr><th width="157">Field</th><th>Description</th></tr></thead><tbody><tr><td>Username</td><td>Username of the person who ran the process.</td></tr><tr><td>Domain</td><td>Domain of the user's computer.</td></tr><tr><td>ID</td><td><p>Indicates the operating system:</p><ul><li>UID for macOS and Linux</li><li>SID for Windows</li></ul></td></tr><tr><td>Earliest Activity</td><td>Timestamp of the earliest tagged item in the Incident Timeline for the user.</td></tr><tr><td>Latest Activity</td><td>Timestamp of the last tagged item in the Incident Timeline for the user.</td></tr></tbody></table>

The following table for **Network Indicators** displays the event logs with the IP addresses that have been tagged.

<table><thead><tr><th width="141">Field</th><th>Description</th></tr></thead><tbody><tr><td>Indicator</td><td>Data field that was tagged.</td></tr><tr><td>Type</td><td><ul><li>IP Address</li><li>Hostname</li><li>URL</li></ul></td></tr><tr><td>Country</td><td>Geolocation data for IP addresses.</td></tr><tr><td>Flag</td><td>Flag of the geolocated country.</td></tr><tr><td>Organization</td><td>Organization associated with the IP address.</td></tr></tbody></table>

The following table for **Data Access** displays all the items that have been tagged in the File Access tables.

<table><thead><tr><th width="137.00006103515625">Field</th><th>Description</th></tr></thead><tbody><tr><td>Path</td><td>Path of the accessed file.</td></tr><tr><td>User</td><td>User name of the person who accessed the file.</td></tr><tr><td>Created</td><td>Creation timestamp of the file accessed.</td></tr><tr><td>Accessed</td><td>Accessed timestamp of the file accessed.</td></tr><tr><td>Modified</td><td>Modified timestamp of the file accessed.</td></tr><tr><td>Size</td><td>Size of the file.</td></tr></tbody></table>
