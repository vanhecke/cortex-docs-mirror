---
description: Explore Response and Remediation playbook use cases in Cortex XSIAM.
---

# Example use cases

The following are examples of Cortex Response and Remediation use cases in Cortex XSIAM.

### **SSO password spray**

* **Detection:** Identifies suspicious login attempts against SSO endpoints.
* **Triage:** The playbook checks the IP reputation and fetches the events related to the SSO login attempts.
* **Early Containment:** The playbook checks if the IP is suspicious. If it is, the playbook suggests blocking the IP.
* **Investigation:**
  * The playbook assesses the risk score of the user who successfully logged in and examines the legitimacy of the user agent.
  * It verifies if the user has MFA configured and analyzes the timestamps of the login attempts to detect potential malicious automated patterns.
* **Containment:**
  * If there is a successful login attempt and the user's risk score is high, or if the user agent is detected as suspicious, or if the time intervals were automated, the playbook clears the user's session.
  * If the user doesn't have MFA, the playbook recommends expiring the user's password.
* **Requirements:** For any response action, you need one of the following integrations:
  * Microsoft Graph User
  * Okta

### **Credential dumping using a known tool**

* **Detection:** Recognizes credential dumping activities.
* **Response:**
  * **Early Containment:** Handles malicious issues by terminating the causality process.
  * **Remediation:** Handles malicious issues by suggesting the analyst to isolate the endpoint. endpoints identified in the detection.

### **User added to local administrator group using PowerShell**

* **Detection:** Detects unauthorized privilege escalations via PowerShell commands.
* **Response:**
  * **Investigation:** Check the following parameters to determine if remediation actions are needed:
    * Cortex XSIAM issues related to the hostname by MITRE tactics indicating malicious activity.
    * Whether the process is unsigned.
  * **Remediation:** Handles malicious issues by terminating the relevant processes and requesting the analyst's approval to remove the user from the local Administrators group. Handles non-malicious issues identified during the investigation.
