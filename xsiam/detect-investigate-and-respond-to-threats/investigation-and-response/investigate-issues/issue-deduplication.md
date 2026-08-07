# Issue deduplication

To optimize issue management and reduce noise, Cortex XSIAM employs a deduplication (dedup) mechanism for specific agent-based issues.

### What is deduplication?

Deduplication is the process of grouping identical security events that occur on the same endpoint within a specific timeframe. Instead of generating a new entry for every recurring instance of a threat, the system consolidates them into a single actionable issue.

### Scope and conditions

Deduplication is strictly applied to issues where the **issue\_name** contains **WildFire** or **Local Analysis**. All other issue types are processed individually and will not be deduped.

### The deduplication key

The system generates a unique fingerprint or key for each incoming issue. If the key matches an existing active issue within the timeframe, the new event is deduped. The formula is as follows:

`{agent_id}_{issue_name}_{hash_id}_{action_status}_{name}_{trigger}`

Key components are resolved using a specific fallback hierarchy to ensure a match even if some data is missing:

<table><thead><tr><th width="168">Component</th><th>Resolution Logic (Fallback Order)</th></tr></thead><tbody><tr><td>hash_id</td><td><code>action_file_sha256 → action_process_image_sha256 → actor_process_image_sha256</code></td></tr><tr><td>name</td><td><code>action_file_name → action_process_image_name → actor_process_image_name</code></td></tr><tr><td>action_status</td><td>Appended only if <code>issue_action_status</code> is present (e.g., Blocked, Detected).</td></tr><tr><td>trigger</td><td>The prevention trigger value from <code>messageData.trigger</code> (if present).</td></tr></tbody></table>

{% hint style="info" %}
### Note

Issues are automatically excluded from deduplication if the `agent_id` is missing, the `hash_id` is missing, or the `hash_id` is an all-zero SHA256 string.
{% endhint %}

### Time-to-live (TTL)

The deduplication window is **1 hour**. This is a sliding window that starts from the ingestion of the first issue. Identical events arriving within this 60-minute buffer are suppressed; events arriving after the window expires will trigger a new issue.

### How to find deduplicated issues

Deduplicated issues are often referred to as "hidden" issues because they do not appear as unique new rows in the issue table. Instead, they are aggregated into the initial "Parent" issue instance.

#### Locating suppressed events

To identify if an issue was suppressed by the dedup logic, search for the primary issue using the following criteria within a **1-hour window before** the timestamp of the expected issue:

* **Agent ID:** Match the specific `agent_id` of the endpoint.
* **Issue Name:** Look for _Local Analysis Malware_ or _WildFire Malware_.
* **File Identification (Hash):** Use the SHA256 hierarchy (Action File → Action Process → Actor Process).
* **File/Process Name:** Match the action\_file\_name or relevant process name.
* **Action Status:** Ensure the issue\_action\_status matches (if it was present on the event).

If you find an issue matching these criteria that occurred less than 60 minutes prior, the "missing" issue has been successfully deduped into that existing entry.
