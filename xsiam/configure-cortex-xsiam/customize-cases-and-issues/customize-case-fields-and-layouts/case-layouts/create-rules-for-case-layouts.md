---
description: >-
  Create Cortex XSIAM case layout rules to apply custom layouts based on case
  severity, source, and other criteria.
---

# Create rules for case layouts

Create Cortex XSIAM case layout rules to apply custom layouts based on case criteria. For example, assign a specific case layout to high-severity cases.

You can create multiple case layout rules. Cortex XSIAM checks each rule until one applies to an incoming case. Content pack layout rules appear first by default. Drag and drop rules to change their order. Filter rules by name, description, rule, layout, or source. If no rule applies, Cortex XSIAM uses the default case layout.

To edit or delete an existing case layout rule, right-click it in the list. Then select **Edit** or **Delete**.

{% hint style="info" %}
Case layout rules support Scope-Based Access Control (SBAC). The following parameters apply to editing access.

* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to restrictive mode, you can edit a rule if you are scoped to all tags in the rule.
* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to permissive mode, you can edit a rule if you are scoped to at least one tag listed in the rule.
* As a scoped user who has editing permissions to a rule, you can change the order among other rules that are locked.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.
{% endhint %}

### Create a Cortex XSIAM case layout rule

1. Select Settings → Configurations → Object Setup → Cases → Layout Rules → **New Rule**.
2. Enter a **Rule Name**, select the custom or out-of-the-box **Layout to Display** if the rule is met, and provide a **Description**.
3. Search for cases matching the case layout rule criteria. For example, search for cases from a specific case source.
4. Click **Create**.
5. Repeat as needed to create multiple rules.
6. Click **Save**.
