# Create rules for case layouts

Case layouts are applied to case according to layout rules. For example, using a layout rule, you can assign a custom case layout based on the case, such as a specific layout for cases with a high severity.

You can create multiple rules. If the first rule does not apply to the incoming case, the next rule is checked, and so on. If a content pack is installed and it contains a layout rule, the layout rule is placed at the top of the rules list, by default. You can change the order of the rules by dragging and dropping the rules in the list. You can filter the rule list by name, description, rule, layout, and source. If no layout rules apply to the case, a default case layout is used.

To edit or delete existing rules, right-click on the rule in the list and select **Edit** or **Delete**.

{% hint style="info" %}
Layout rules support SBAC (scoped based access control). The following parameters are considered for editing access.

* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to restrictive mode, you can edit a rule if you are scoped to all tags in the rule.
* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to permissive mode, you can edit a rule if you are scoped to at least one tag listed in the rule.
* As a scoped user who has editing permissions to a rule, you can change the order among other rules that are locked.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.
{% endhint %}

#### How to create rules for case layouts

1. Select Settings → Configurations → Object Setup → Cases → Layout Rules → **New Rule**.
2. Enter a **Rule Name**, select the custom or out-of-the-box **Layout to Display** if the rule is met, and provide a **Description**.
3. Search for cases that match the criteria you want to use for the layout rule. For example, you can search for cases from a specific case source.
4. Click **Create**.
5. Repeat as needed to create multiple rules.
6. Click **Save**.
