---
description: Configure Exception Management Admin permissions in Cortex XSIAM.
---

# Exception Management Admin permissions

Exception Management Admin controls access to the **Exception Rules** tab on the **Issue Exclusions and Exceptions** page under **Settings** → **Issue Exception & Exclusion**. Exception rules differ from exclusion rules in that they define conditions under which issues are flagged as exceptions that may require approval before being acted upon, rather than being silently suppressed.

{% hint style="info" %}
Requires **Issue Exclusions** permission (at least View) to access the page. Without Issue Exclusions, the entire page is hidden.
{% endhint %}

| Permission | Description                                                                                                                                                                                                                                                                                 | Roles Example                                                                                                                                                    |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to the **Exceptions Rules** tab on the **All Issue Exception & Exclusion Rules** page.                                                                                                                                                                                            | SOC Tier-1 Analyst: Should escalate false positives rather than create an exception.                                                                             |
| View       | Read-only access to the Exception Rules tab on the**All Issue Exception & Exclusion Rules** page. Users can browse Exception Rules, view rule details including BIOC indicator definitions, and filter/search the exception rules grid, but cannot create, edit, or delete exception rules. | SOC Tier-2 Analyst and Threat Hunter: Should reference existing exceptions during investigations or understand filtered activity.                                |
| View/Edit  | Read and write access to **the Exception Rules** tab on the**All Issue Exception & Exclusion Rules** page, including creating, editing, and deleting Exception Rules.                                                                                                                       | <ul><li>SOC Tier-3 Analyst: Create exception rules for validated false positives.</li><li>Security Engineer: Manage exception rules as part of tuning.</li></ul> |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission       | Permission Level  | Reason                                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cases & Issues   | View              | Exception rules are based on issue attributes. Without alert visibility, users cannot understand the context of what is being excepted. Required.                                                                                                                                                                                                                                                                     |
| Issue Exclusions | View or View/Edit | <ul><li>View: Issue Exclusions is a prerequisite. Controls access to the <strong>All Issue Exclusions and Exceptions</strong> page. Without it, the page is hidden, and the Exception Rules tab cannot be reached. Required.</li><li>View/Edit: Users who manage exception rules typically also need to manage exclusion rules. Having both at View/Edit provides a complete exception management workflow.</li></ul> |
