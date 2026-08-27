---
description: Monitor Cortex XSIAM hunt searches and results across targeted endpoints.
---

# Hunt status

Hunts consist of searches across multiple endpoints and those searches can take time to return results from all of the targeted endpoints. To view the status of all of the searches contained within a hunt, go to **Investigation & Response** → **Forensics**. From the investigations table, click the investigation link. From the **Collections** tab, select **Hunt** and from the **Status** column of the hunt, click **Actions**. This launches a new browser tab displaying the **Actions** table. Within the **Actions** table, you can scroll or use the filters to see the status of any search within a hunt across any of the targeted endpoints.

Using this information, you can identify the successful and failed searches and take the necessary action in Cortex XSIAM.

<table><thead><tr><th width="145">Field</th><th>Description</th></tr></thead><tbody><tr><td>Endpoint name</td><td>Agent hostname.</td></tr><tr><td>Endpoint ID</td><td>Agent unique ID.</td></tr><tr><td>Action ID</td><td>A unique identifier for the agent action.</td></tr><tr><td>Name</td><td>Name of search.</td></tr><tr><td>Status</td><td><p>Shows one of the following statuses of the search:</p><ul><li>Pending</li><li>In progress</li><li>Completed successfully</li><li>Failed</li><li>Timeout</li></ul></td></tr><tr><td>Artifact category</td><td><p>Name of category for the search.</p><p>Example: <code>Process execution</code></p></td></tr><tr><td>Artifact</td><td><p>Artifact targeted by this search.</p><p>Example: <code>Amcache</code></p></td></tr><tr><td>Results</td><td>Number of results received for the search.</td></tr><tr><td>Last updated</td><td>Latest time results were received for this action.</td></tr><tr><td>Parameters</td><td><p>The string that describes the search parameters.</p><p>Example: <code>C:\Users* File Name Regex: *.exe</code></p></td></tr><tr><td>Creation time</td><td>Timestamp when the search was created.</td></tr></tbody></table>
