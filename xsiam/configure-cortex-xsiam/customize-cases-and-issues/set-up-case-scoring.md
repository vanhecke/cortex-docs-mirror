---
description: Enable SmartScore and configure scoring rules for cases and issues.
---

# Set up case scoring

To set up case scoring, you need to enable SmartScore and enable and define scoring rules.

### Enable SmartScore

To set up case scoring, you need to enable SmartScore and enable and define scoring rules.

1. Select Settings → Configurations → **Cortex XSIAM- Analytics** and click **Enable**.
2. Select Cases & Issues → Case Configuration → **Case Scoring** and enable **SmartScore**.

{% hint style="info" %}
### Note

On the first activation, it can take up to 48 hours for SmartScore to calculate and display the score.

Enabling SmartScore subsequently impacts the User Score.
{% endhint %}

### Enable and define scoring rules

1.  Select Cases & Issues → Case Configuration → Case Scoring → Scoring Rules and enable User Scoring Rules.

    The Scoring Rules table displays the user-defined rules and sub-rules.
2. Click Add Scoring Rule.
3.  In the Create New Scoring Rule dialog, define the rule criteria:

    1. Under Rule Name, enter a unique name for your rule.
    2. Under Score, define the score that Cortex XSIAM should apply to issues that matching the rule criteria.
    3. Under Base Rule, select whether to create a top-level rule (labeled Root) or a sub-rule (labeled _Rule Name (ID:#)_). By default, rules are defined at the root level.
    4.  Select or deselect Apply score only to first issue of case.

        By selecting this option you choose to apply the score only to the first issue that matches the defined rule. Subsequent issues of the same case will not receive a score from this rule. By default, a score is applied only to the first issue that matches the defined rule and sub-rule.
    5.  In the issue table, use the filters to define the attributes you want to include in the rule match criteria. For example, you can select issues with High severity, issues by category, or issues associated with certain assets or asset providers.

        Right-click an issue field to add it as match criteria.

    Example: With this rule, Cortex XSIAM assigns a score of 30 to any XDR BIOC issues with a severity level of Critical:

    * Score = 30
    * Base Rule = Root
    *   Filters:

        `Issue Source=XDR BIOC AND Severity=Critical`

    <br>
4.  Click Create.

    You are automatically redirected to the Scoring Rules table.
5.  In the Scoring Rules table, click Save to save your scoring rule.

    For scoped users, a small lock icon indicates that you don't have permissions to edit a rule.

### Revise existing scoring rules

In the Scoring Rules table, take the following actions to review your rules and sub-rules:

* Use the arrows to rearrange rule priorities. Make sure to click Save after any changes.
* Select one or more rules and right-click to see the available actions.

### Scope-Based Access Control Considerations

Case Scoring supports Scope-Based Access Control (SBAC). If you're a scoped user, a small lock icon indicates that you don't have permissions to edit a rule. The following parameters are considered when editing a scoring rule:

* If Scope-Based Access Control (SBAC) is enabled and Endpoint Scoping Mode is set to restrictive mode, you can edit a rule if you are scoped to all tags in the rule.
* If Scope-Based Access Control (SBAC) is enabled and Endpoint Scoping Mode is set to permissive mode, you can edit a rule if you are scoped to at least one tag listed in the rule.
* To change the order of a rule, you must have permissions to the other rules of which you want to change the order.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.
