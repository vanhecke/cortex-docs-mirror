---
description: Create rules that automatically star matching issues and their linked cases.
---

# Create a starring configuration

You can proactively star issues and the cases to which they are linked by creating a starring configuration:

1. Select Cases & Issues → Case Configuration → **Starred Issues**.
2. Select **Add Starring Configuration**.
3. Under **Configuration Name**, enter a name to identify your starring configuration.
4. (Optional) Under **Comment**, enter a descriptive comment.
5.  In the issue table, use the filters to define the issue attributes you want to include in the match criteria. For example, you can select issues with High severity, issues by category, or issues associated with certain assets or asset providers.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>Right-click an issue field to add it as match criteria.</p></div>
6. Click **Create**.

<details>

<summary>Scope-Based Access Control considerations</summary>

Case starring supports Scope-Based Access Control (SBAC). The following parameters are considered when editing a starring configuration:

* If **Scope-Based Access Control (SBAC)** is enabled and the **Endpoint Scoping Mode** is set to restrictive mode, you can edit a configuration if you are scoped to all tags in the configuration.
* If **Scope-Based Access Control (SBAC)** is enabled and the **Endpoint Scoping Mode** is set to permissive mode, you can edit a configuration if you are scoped to at least one tag listed in the configuration.
* If a policy was added when set to restrictive mode, and then changed to permissive (or vice versa), you will only have view permissions.

</details>
