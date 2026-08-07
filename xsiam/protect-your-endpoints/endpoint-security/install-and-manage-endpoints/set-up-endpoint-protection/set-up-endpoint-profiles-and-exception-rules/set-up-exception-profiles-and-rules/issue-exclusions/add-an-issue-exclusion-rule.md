# Add an issue exclusion rule

Through the process of triaging issues or resolving a case, you may determine that a specific issue does not indicate a threat. If you want Cortex XSIAM to exclude the display of issues that match certain criteria, you can create an issue exclusion rule.

After you create an exclusion rule, Cortex XSIAM hides any future issues that match the criteria, and excludes the issues from cases and search query results. If you choose to apply the rule to historic results as well as future issues, the app marks any historic issues as unavailable.

{% hint style="info" %}
### Note

If a case only contains issues with exclusions, Cortex XSIAM changes the case status to **Resolved - False Positive** and sends an email notification to the issue assignee (if set).
{% endhint %}

There are two ways to create an exclusion rule. You can define the exclusion criteria when you investigate a case, or you can create an issue exclusion from scratch.

{% hint style="info" %}
### Note

You can also set up issue exceptions by creating global endpoint policy exceptions. For more information, see [Add a global endpoint policy exception](../add-a-legacy-exception-rule-for-endpoints/add-a-global-endpoint-policy-exception).
{% endhint %}

Issue exclusions support Scope-Based Access Control (SBAC). For more information, see [Manage user scope](../../../../../../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-user-scope).

The following parameters are considered when editing a rule:

* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to restrictive mode, you can edit a rule if you are scoped to all tags in the rule.
* If **Scope-Based Access Control (SBAC)** is enabled and **Endpoint Scoping Mode** is set to permissive mode, you can edit a rule if you are scoped to at least one tag listed in the rule.
* If a rule was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.

<details>

<summary>Build an issue exclusion policy from issues in a case</summary>

If after reviewing the case details, you want to suppress one or more issues from appearing in the future, create an exclusion policy based on the issues in the case. When you create a case from the **Cases** view, you can define the criteria based on the issues in the case. If desired, you can also create an issue exclusion policy from scratch.

1. On the **Cases** page, expand the case, click the case's menu icon and, select **Create Exclusion**.
2. Enter a name for your issue exclusion rule.
3. Describe the reason or purpose of the rule.
4.  Use the issue filters to add any match criteria for the issue exclusion policy.

    You can also right-click a specific value in the issue to add it as match criteria. The app refreshes, to show you which issues in the case will be excluded. To see all matching issues, including those not related to the case, clear the option to **Show only issues** in the named case.
5.  Click **Create** to create the exclusion rule and confirm the action.

    If you need to make changes later, you can view, modify, or delete the exclusion rule from the **Settings** → **Exception Configuration** → **Issue Exclusions** page.

</details>

<details>

<summary>Build an issue exclusion rule from scratch</summary>

Build your own issue exclusion rule.

1. Select **Settings** → **Exception Configuration** → **Issue Exclusions**.
2. Select **+ Add an Issue Exclusion Rule**.
3. Enter a name for your issue exclusion rule.
4. Describe the reason or purpose of the rule.
5.  Define the exclusion criteria.

    * Use the filters at the top of the table to build your exclusion criteria.
    * Use existing issue values to populate your exclusion criteria. To do so, right-click the column value on which you want to base your rule, and select **Add issues with \<value> to configuration**.

    As you define the criteria, the app filters the results to display matches.
6.  Review the results.

    The issues in the table will be excluded from appearing in the app after the rule is created, and optionally, any existing issue matches will be displayed as unavailable.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Caution</h3><p>This action is irreversible. All historically excluded issues will remain excluded if you disable or delete the rule.</p></div>
7. Click **Create** to create the issue exception rule.

</details>
