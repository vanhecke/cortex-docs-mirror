# Create rules for issue layouts

Issue layouts are applied to issues according to layout rules. Using a layout rule, you can assign a custom issue layout based on the issue source, such as a specific layout for issues generated from a correlation rule.

You can create multiple rules. If the first rule does not apply to the incoming issue, the next rule is checked, and so on. If a content pack is installed and it contains a layout rule, by default the layout rule is placed at the top of the rules list. You can change the order of the rules by dragging and dropping the rules in the list. You can filter the rule list by name, description, rule, layout, and source. If no layout rules apply to the issue, a default issue layout is used.

To edit or delete existing rules, right-click on the rule in the list and select Edit or Delete.

### How to create layout rules

1. Go to Settings → Configurations → Object Setup → Issues → Layout Rules → New Rule.
2. Enter a rule name, select the layout to use if the rule is met, and provide a description.
3. Search for issues that match the criteria you want to use for the layout rule. For example, you can search for issues from a specific issue source.
4. Click Create.
5. Repeat as needed to create multiple rules.
6. Click Save.

### **SBAC considerations**

Layout rules support SBAC (scoped based access control). The following parameters are considered for editing access.

* If Scope-Based Access Control (SBAC) is enabled and Endpoint Scoping Mode is set to restrictive mode, you can edit a rule if you are scoped to all tags in the rule.
* If Scope-Based Access Control (SBAC) is enabled and Endpoint Scoping Mode is set to permissive mode, you can edit a rule if you are scoped to at least one tag listed in the rule.
* As a scoped user who has editing permissions to a rule, you can change the order among other rules that are locked.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.
