---
description: >-
  Create Cortex XSIAM starring rules to automatically prioritize matching issues
  and their linked cases.
---

# Create a starring configuration

Create a Cortex XSIAM starring configuration to automatically flag priority issues and linked cases. Define issue-based criteria to focus investigations on the most relevant cases.

### Create an issue and case starring rule

1. Select Cases & Issues → Case Configuration → **Starred Issues**.
2. Select **Add Starring Configuration**.
3. Under **Configuration Name**, enter a name for the issue and case starring rule.
4. (Optional) Under **Comment**, enter a descriptive comment.
5.  In the issue table, use the filters to define the issue attributes you want to include in the match criteria. For example, you can select issues with High severity, issues by category, or issues associated with certain assets or asset providers.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>Right-click an issue field to add it as match criteria.</p></div>
6. Click **Create**.

<details>

<summary>Scope-Based Access Control for starring configurations</summary>

Case starring supports Scope-Based Access Control (SBAC). The following parameters apply when you edit a starring configuration:

* If **Scope-Based Access Control (SBAC)** is enabled and the **Endpoint Scoping Mode** is set to restrictive mode, you can edit a configuration if you are scoped to all tags in the configuration.
* If **Scope-Based Access Control (SBAC)** is enabled and the **Endpoint Scoping Mode** is set to permissive mode, you can edit a configuration if you are scoped to at least one tag listed in the configuration.
* If a policy was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.

</details>
