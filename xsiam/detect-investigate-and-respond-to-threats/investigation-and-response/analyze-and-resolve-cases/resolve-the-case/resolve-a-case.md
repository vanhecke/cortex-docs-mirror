---
description: Resolve Cortex XSIAM cases manually, through playbooks, or with the API.
---

# How to resolve a case

In Cortex XSIAM you can resolve a case in the following ways:

* Manually on the **Cases** page:
  * Click the case status and select **Resolved**.
  * In the **Resolve case** dialog, select the resolution reason and leave a comment.
  * Select whether to resolve all of the issues in the case, and whether to create an exclusion.
  * Click **Resolve**.
* In the **War Room** or as a playbook task. Run the `!setParentIncidentFields` command.
* In the API, run the `Update Case` command .

{% hint style="info" %}
### Note

If a case is resolved with the status `Resolved - Auto Resolved`, Cortex XSIAM can reopen the case for up-to six hours if a new issue is triggered that matches the case. The six-hour period is defined by the timestamp of the last issue that was grouped into the case. After the six-hour period, any new issues are linked to a new case for a new investigation.
{% endhint %}
