---
description: >-
  Create Cortex XSIAM managed security actions for child tenants, including
  issues exclusions, starred isses, and endpoint profiles.
---

# Create a security managed action

After you have created and assigned a configuration for each of your child tenant’s security actions, you can define the specific managed action on behalf of the child tenant.

1. Navigate to each of the following Cortex XSIAM pages and follow the detailed steps:
   * Settings → Issue Exception and Exclusion → **All Issue Exception &** **Exclusion Rule** page.
   * Case & Issues → Case Configuration → Starred Issues → **Starred Issues** page.
   * Inventory → Endpoints → Policy Management → Prevention → Profiles → **Prevention Profiles** page.
   * Investigation & Response → Response → Action Center → Applied Actions → Block List/Allow List → **Allow List/Block List** page.
2.  In the corresponding **Configuration** panel, select the [action configuration](create-and-allocate-configurations) you created and allocated to your child tenant.

    The corresponding security action **Table** displays the actions managing the child tenant.
3.  Depending on the security action, select:

    * Add an exclusion to create an issue exclusion.
    * Add a starring configuration to create a starred issue inclusion.
    * Add a new profile to create a new endpoint profile.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Profiles you create are automatically cloned to your child tenants.</p></div>
