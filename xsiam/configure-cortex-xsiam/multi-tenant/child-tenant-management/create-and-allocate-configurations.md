---
description: >-
  Create and assign Cortex XSIAM security action configurations to centrally
  manage issues, profiles, and allowlists for child tenants.
---

# Create and allocate configurations

To manage security actions on behalf of your child tenant, you need to first create and allocate an action configuration.

1. Navigate to each of the following Cortex XSIAM pages and follow the detailed steps:
   * Settings → Issue Exception and Exclusion → **All Issue Exception &** **Exclusion Rule** page.
   * Case & Issues → Case Configuration → Starred Issues → **Starred Issues** page.
   * Inventory → Endpoints → Policy Management → Prevention → Profiles → **Prevention Profiles** page.
   * Investigation & Response → Response → Action Center → Applied Actions → Block List/Allow List → **Allow List/Block List** page.
2. On the corresponding page, add the relevent configuration.
3. Enter the configuration **Name** and **Description**.
4.  **Create**.

    The new configuration appears in the **Configuration** pane.
5. Navigate to Settings → **Tenant Management**.
6. In the **Tenant Management** table, right-click a child tenant row and **Edit Configurations**.
7.  Assign the configuration you want to use to manage each of the security actions.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can configure <strong>Profiles</strong> only as <strong>Managed</strong> or <strong>Unmanaged</strong>. All profiles you create are automatically cloned to your child tenants.</p></div>
8.  **Update**.

    The **Tenant Management** table is updated with your assigned configurations.
