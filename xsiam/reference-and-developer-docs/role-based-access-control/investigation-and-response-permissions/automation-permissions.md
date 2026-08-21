---
description: >-
  Configure permissions for playbooks, scripts, playground, and automated
  exclusions in Cortex XSIAM.
---

# Automation permissions

This section covers permissions for playbooks, scripts, playground, and the Automated Exclusion Center.

* [playbook-permissions](automation-permissions/playbook-permissions "mention")
* [script-permissions](automation-permissions/script-permissions "mention")
* [jobs-permissions](automation-permissions/jobs-permissions "mention")
* [playground-permissions](automation-permissions/playground-permissions "mention")
* [automation-exclusion-center-permissions](automation-permissions/automation-exclusion-center-permissions "mention")

{% hint style="warning" %}
### Caution

Cortex XSIAM enforces a strict permission dependency chain for automation and case management. You must grant at least View access to Scripts before you can grant access to Playbooks. Consequently, you must grant at least View access to Playbooks before you can enable Cases & Issues.
{% endhint %}
