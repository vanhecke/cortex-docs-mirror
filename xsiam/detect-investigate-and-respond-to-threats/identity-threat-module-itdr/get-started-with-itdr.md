---
description: >-
  Get started with Cortex XSIAM Identity Threat Detection and Response to
  protect identities and investigate threats.
---

# Get started with ITDR

To deploy and configure the Identity Threat Detection and Response module features, follow the steps below.

1. Activate the ITDR add-on license from **Settings -> Cortex XSIAM License**. This activates the identity analytics features automatically.
2. Activate and onboard the [Cloud Identity Engine](https://docs.paloaltonetworks.com/identity/activation-and-onboarding/get-started-with-the-cloud-identity-engine).
3. Set up the dedicated Identity permissions and roles in **Settings -> Configurations -> Access Management -> Roles -> Identity Security**. For more information, see [RBAC in ITDR](manage-role-based-access-control-rbac-in-itdr).
4. Configure Identity Profiles to unify AD-SPM, Conditional Access, and LDAP Protection controls in one centralized hub.

## Set up Identity Profiles

The Identity Profile centralizes identity security policies for Domain Controllers. It supports consistent security controls across your environment. After configuration, the profile must be mapped to policies for Domain Controller endpoints.

{% hint style="info" %}
### Note

Identity Profile requires Cortex XSIAM 3.5, Cortex XDR 5.1, or Cortex Cloud Runtime 2.1 or later. It also requires Cortex XDR agent 9.1 or later. It is unavailable for Cortex XSIAM 2.x and Cortex XDR 3.x tenants.

Policies can contain an Identity Profile in mixed-agent environments. Agents earlier than version 9.1 ignore these settings.

Identity Profile is available in Windows endpoints.
{% endhint %}

To customize settings for specific agents, create an Identity Profile and assign it to policy rules for Domain Controller endpoints.

1. Add a profile and define its basic settings.
   1.  Go to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**. Select **+ Add Profile**, then select whether to create or import a profile.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Imported profiles are added. They do not replace existing profiles.</p></div>
   2. Select the **Windows** platform and **Identity** profile type.
   3. Click **Next**.
   4. Enter a unique **Profile Name**. Use only letters, numbers, or spaces. Names must contain 30 characters or fewer.
   5. Add a **Description** with the profile's purpose or business reason. For example, include a case ID or help desk ticket link.
2.  Use the toggle to enable or disable **AD-SPM**.\
    Use **Active Directory Security Posture Management** to monitor Active Directory for risky account configurations, weak or compromised passwords, unused accounts, and excessive privileges. Use Weak Password to identify weak passwords used in Active Directory and define the scan frequency.

    When enabled, both **Weak Password** and **AD-SPM** are both enabled.
3.  Use the toggle to enable or disable **Conditional Access**. When enabled, configure these options:

    | Item                           | Options                       | More details                                                                                                                                                                                                                           |
    | ------------------------------ | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Silent Logging Mode            | `On` `Off`                    | When set to **On**, you can observe the impact of this profile before enforcing policies.                                                                                                                                              |
    | Service Availability Fail-Mode | `Allow Access` `Block Access` | Defines global system behavior when the entire Conditional Access service is unavailable and rule evaluation is impossible. **Allow Access** minimizes disruption and helps prevent user lockout. **Block Access** maximizes security. |
    | Conditional Access Policy      | —                             | Open the **Identity Access Rules** page to view or change current Conditional Access policies.                                                                                                                                         |
4.  Configure **LDAP Protection** to analyze and act on suspicious LDAP queries sent to Domain Controllers. This feature detects and blocks Active Directory reconnaissance attacks. Use the toggle to enable or disable it.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>LDAP Protection takes effect after an agent restart.</p></div>

    | Item                                              | Options                 | More details                                                                                                     |
    | ------------------------------------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------- |
    | Action Mode                                       | Block, Report, Disabled | The Cortex XDR agent performs this action when it detects suspicious Domain Controller queries.                  |
    | Monitor and Collect Domain Controller LDAP Events | Enabled, Disabled       | When enabled, the agent collects LDAP query information and creates events for investigating suspicious queries. |
5. Click **Create** to save the profile.

### What to do next

Apply the new profile by adding it to a policy rule. You can also define other profiles first. Policy rules let you select the endpoints that receive the policy.
