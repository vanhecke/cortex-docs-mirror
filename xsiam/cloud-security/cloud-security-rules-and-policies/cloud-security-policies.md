---
description: Learn about cloud security policies in Cortex XSIAM.
---

# Cloud security policies

Cloud security policies allow you to define the scope of assets for which to create issues when a rule matches.

While cloud security rules provide the detection logic (defining _what_ to detect), cloud security policies provide the context (defining _where_ to apply the rule) and enforcement (_what_ to do when the rule is triggered).

A cloud security policy consists of:

* **Rules:** Select from a list of security detection rules or create a new rule.
* **Scope:** Filter which assets the rule applies to.

On their own, cloud security rules create findings across all assets. But when a rule is associated with a policy, for the assets within the scope of that particular rule, the findings are promoted to issues.

While cloud security rules establish the criteria for evaluation but do not initiate any actions unless incorporated within a policy, cloud security policies serve as enforcement mechanisms that govern the responses to the identified findings.

<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-0f6bec299ad0cfa7aea5f975c84b0df3251fd7c2%2F32334dc22cc4793cc6c6d424ae85d976f757f6383c4036f9432ef9f4ae5e1999.png?alt=media" alt="image2.png" width="375">

The Cloud Posture Security Policies page allows you to manage policies that define security and compliance actions for cloud posture. You can create, edit, filter, and manage policies through a structured table and widget panel.

{% hint style="info" %}
### Note

If you have the following Scope Based Access Control (SBAC) settings in place, **User Settings** → **Cases and Issues Scope** → **Select domains** → **Posture**, you may encounter a Case mismatch in Issues/Cases/Findings counts. This is because the Case count on the Rules page captures Cases belonging to the Posture domain. Whereas Platform pages, capture Issues within Cases belonging to the Posture domain.
{% endhint %}

**Default Cloud Posture Security Policy**

The _Default Cloud Posture Security Policy_ is an out-of-the-box (OOTB) policy that evaluates your environment against out-of-the-box detection rules. These default rules are rule-based and heuristic-based (using AI and machine learning), drawing on security research, CIS benchmarks, customer requests, and Palo Alto Networks' internal threat research.

The _Default Cloud Posture Security Policy_ is enabled by default, but can be disabled and enabled as needed.

**Custom cloud security policies**

If instead of using the default cloud security policy you prefer to define your own, you can define custom cloud security policies.

**Issues**

Issues are artifacts of the policy and represent actionable items that you need to address. A key distinction between findings and issues is that findings are not actionable, while you can take action on issues.

For more information about issues, see [Issues, findings, and events](../../detect-investigate-and-respond-to-threats/investigation-and-response/case-concepts/issues-findings-and-events) and [Investigate issues](https://app.gitbook.com/s/ocwvgxtzkvBHMLbPsZuG/detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues).
