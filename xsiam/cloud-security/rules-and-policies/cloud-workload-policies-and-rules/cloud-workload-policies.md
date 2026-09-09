---
description: >-
  Configure Cortex XSIAM cloud workload policies to detect violations, create
  issues, and prevent risks across SDLC stages.
---

# Cloud workload policies

Cloud Workload Policies help you prevent and manage security violations in your cloud runtime instances. They enable you to apply detection logic to specific asset groups at the desired SDLC stage, and define what action needs to be taken if the conditions are met.

Depending on the nature of the security violation, a Cloud Workload Policy allows you to

* _Prevent the violation_. Enable proactive prevention of the violation. For example: Block an S3 bucket deployment that is open to the public.
* _Create an issue_. Create an issue when violation is seen. For example: Create an issue when an AWS credential file is found on a Linux server.

{% hint style="info" %}
### Note

Issues are automatically resolved when the finding is no longer applicable to the asset or when the affected asset is removed from the inventory.

For more details on Prevent and create issues, see [Cloud Workload Preventive Action](cloud-workload-policies/cloud-workload-preventive-action).
{% endhint %}

A Cortex Cloud Workload Policy has the following elements:

* **SDLC Evaluation Stage:** The SDLC stage at which the policy is applied and evaluated. Depending on the policy type, one or more of the following stages may be available:
  * **CI:** The stage during which a pipeline builds the artifact. After building the artifact, the pipeline pushes it to a registry.
  * **Deploy:** The stage when the artifact is pushed to a cloud instance for running.
  * **Runtime:** The stage when the artifact is running on a cloud instance.
* **Rule (Conditions):** The logical conditions that will trigger the evaluation of this policy.
* **Scope:** A filter specifying which assets the rule applies to.
* **Action:** The response triggered when the rule evaluates successfully (only when part of a policy). Based on the rules included in the policy, it can create an issue or prevent the security violation.
