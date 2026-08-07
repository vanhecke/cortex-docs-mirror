---
description: View and use context data stored for a case.
---

# Case context data

Context data is written to issues and not to cases. Therefore, the case context might be empty unless you previously added context data to the case.

To see context data for a case, open a case, click the Actions menu and select **View context data**.

Adding context data from issues to a parent case can help you with the following tasks:

*   **Remediation**: You can add context data from an issue, such as the issue status, actions, or ID, to its parent case's context data. This allows other playbooks to use the parent case context.

    For example, if you have multiple issues in a case, you can add context data from each of the issues to the parent case. You can then use the case context data in playbooks and avoid running duplicate actions on the issues.
* **Case assignment**: You can see if an analyst has been assigned to the case or other issues.
* **Insights at the case level**: For automation engineers, you can set responses based on characteristics in the case.

For more information, see [Add context data to a case](add-context-data-to-a-case).
