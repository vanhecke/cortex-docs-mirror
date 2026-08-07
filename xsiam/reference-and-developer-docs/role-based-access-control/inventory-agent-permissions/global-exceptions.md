# Global Exceptions

Global Exceptions allow security teams to exclude specific items from detection, such as creating hash-based exceptions (SHA256, MD5) and defining path-based exceptions for files and folders.

{% hint style="info" %}
### Note

Global Exceptions are part of the Prevention section and apply to prevention policies/profiles.
{% endhint %}

{% hint style="warning" %}
### Caution

Global Exceptions can significantly impact security coverage. Implement approval workflows and regular exception reviews. Consider requiring dual approval for exception creation.
{% endhint %}

| Permissions | Description                                                                                                                                                                                   | Roles Example                                                                                                                                                                                                                                                                                                                        |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| None        | Cannot view the Global Exceptions menu (**Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Global Exceptions**, and cannot create an exception from an issue or case. |                                                                                                                                                                                                                                                                                                                                      |
| View        | Read-only access for the Global Exceptions menu, and cannot create an exception from an issue or case.                                                                                        | <ul><li>SOC Tier-1 Analyst: Understanding exceptions helps explain why certain files weren't blocked.</li><li>SOC Tier-2 Analyst: Exception visibility is critical for understanding why threats may have bypassed protection.</li><li>Threat Hunter: Exceptions represent potential blind spots. Hunters need visibility.</li></ul> |
| View/Edit   | All view permissions plus managing exceptions, adding an exception from an issue or case, setting exception expiration, and defining execution scope.                                         | <ul><li>SOC Tier 3 Analyst: May need temporary exceptions for remediation, requires approval.</li><li>Security Engineer: Responsible for exception management with proper documentation.</li></ul>                                                                                                                                   |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission                | Permission Level | Reason                                                                                                                                                                                                                                            |
| ------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agent Prevention Policies | View             | Required to view policies where exceptions apply.                                                                                                                                                                                                 |
| Cases & Issues            | View             | Recommended. Exceptions are often created in response to false positives from cases/issues. Case context helps understand exception justification. View/Edit is required, as the Add Exception action appears in the Case and Issue context menu. |
| Agent Administrations     | View             | Strongly recommended to view endpoints to assess the scope of exceptions. Helps determine if an exception should be global or targeted.                                                                                                           |
| Agent Groups              | View             | Required. Exceptions can be scoped to specific groups. Group visibility is needed to target exceptions appropriately.                                                                                                                             |
| Agent Profiles            | View             | Recommended. Understanding profile settings helps determine if an exception is needed or if a profile adjustment would be more appropriate.                                                                                                       |
