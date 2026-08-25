---
description: >-
  Configure identity profiles for endpoint-related identity protection settings
  in Cortex XSIAM.
---

# Set up Identity profiles

Configure the Identity Profile to unify AD-SPM, Conditional Access, and LDAP Protection controls in one centralized hub.

{% hint style="warning" %}
Requires the ITDR add-on.
{% endhint %}

The Identity Profile centralizes identity security policies for Domain Controllers. It supports consistent security controls across your environment. This Windows-only profile must be mapped to policies for Domain Controller endpoints.

{% hint style="info" %}
### Note

Identity Profile requires Cortex XSIAM 3.6 or later and Cortex XDR agent 9.1 or later.&#x20;

Policies can contain an Identity Profile in mixed-agent environments. Agents earlier than version 9.1 ignore these settings.
{% endhint %}

To customize settings for specific agents, create an Identity Profile and assign it to policy rules for Domain Controller endpoints.

1. Add a profile and define its basic settings.
   1.  Go to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Select **+ Add Profile**, then select whether to create or import a profile.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Imported profiles are added. They do not replace existing profiles.</p></div>
   2. Select the **Windows** platform and **Identity** profile type.
   3. Click **Next**.
   4. Enter a unique **Profile Name**. Use only letters, numbers, or spaces. Names must contain 30 characters or fewer.
   5. Add a **Description** with the profile's purpose or business reason. For example, include a case ID or help desk ticket link.
2.  Configure **LDAP Protection** to analyze and act on suspicious LDAP queries sent to Domain Controllers. This feature detects and blocks Active Directory reconnaissance attacks. Use the toggle to enable or disable it.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>LDAP Protection takes effect after an agent restart.</p></div>

    | Item                                              | Options                 | More details                                                                                                     |
    | ------------------------------------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------- |
    | Action Mode                                       | Block, Report, Disabled | The Cortex XDR agent performs this action when it detects suspicious Domain Controller queries.                  |
    | Monitor and Collect Domain Controller LDAP Events | Enabled, Disabled       | When enabled, the agent collects LDAP query information and creates events for investigating suspicious queries. |
3. Click **Create** to save the profile.

### What to do next

Apply the new profile by adding it to a policy rule. You can also define other profiles first. Policy rules let you select the endpoints that receive the policy.

<details>

<summary>Create a policy rule from the Prevention Profiles page</summary>

1. Go to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**.
2. Right-click the new profile and select **Create a new policy rule using this profile**.
3. Configure the policy rule.

</details>

<details>

<summary>Edit an existing policy rule from the Policy Rules page</summary>

1. Go to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Policy Rules**.
2. Right-click an existing policy and select **Edit**.
3. Add the new profile to the policy rule.

</details>

<details>

<summary>Create a new policy rule from the Policy Rules page</summary>

1. Go to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Policy Rules**.
2. Click **Add Policy**.
3. Configure a policy that includes the new profile.

</details>
