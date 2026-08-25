---
description: >-
  Configure Cortex XSIAM case scoring with SmartScore and user-defined scoring
  rules for cases and issues.
---

# Set up case scoring

Set up Cortex XSIAM case scoring to prioritize cases and issues. Enable SmartScore and configure user-defined scoring rules that match your investigation criteria.

### Enable Cortex XSIAM SmartScore

Enable SmartScore before you configure Cortex XSIAM case scoring rules.

1. Select Settings → Configurations → **Cortex XSIAM- Analytics** and click **Enable**.
2. Select Cases & Issues → Case Configuration → **Case Scoring** and enable **SmartScore**.

{% hint style="info" %}
On the first activation, it can take up to 48 hours for SmartScore to calculate and display the score.

Enabling SmartScore subsequently impacts the User Score.
{% endhint %}

### Create case and issue scoring rules

1.  Select Cases & Issues → Case Configuration → Case Scoring → Scoring Rules and enable User Scoring Rules.

    The Scoring Rules table displays the user-defined rules and sub-rules.
2. Click Add Scoring Rule.
3. In the Create New Scoring Rule dialog, define the rule criteria:
   * Score = 30
   * Base Rule = Root
   *   Filters:

       `Issue Source=XDR BIOC AND Severity=Critical`
4.  Click Create.

    You are automatically redirected to the Scoring Rules table.
5.  In the Scoring Rules table, click Save to save your scoring rule.

    For scoped users, a small lock icon indicates that you don't have permissions to edit a rule.

### Manage existing case scoring rules

In the Scoring Rules table, take the following actions to review your rules and sub-rules:

* Use the arrows to rearrange rule priorities. Click Save after any changes.
* Select one or more rules and right-click to see the available actions.

### Scope-Based Access Control for case scoring

Case scoring supports Scope-Based Access Control (SBAC). If you're a scoped user, a small lock icon indicates that you cannot edit a rule. The following parameters apply when you edit a scoring rule:

* If Scope-Based Access Control (SBAC) is enabled and Endpoint Scoping Mode is set to restrictive mode, you can edit a rule if you are scoped to all tags in the rule.
* If Scope-Based Access Control (SBAC) is enabled and Endpoint Scoping Mode is set to permissive mode, you can edit a rule if you are scoped to at least one tag listed in the rule.
* To change the order of a rule, you must have permissions to the other rules of which you want to change the order.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.
