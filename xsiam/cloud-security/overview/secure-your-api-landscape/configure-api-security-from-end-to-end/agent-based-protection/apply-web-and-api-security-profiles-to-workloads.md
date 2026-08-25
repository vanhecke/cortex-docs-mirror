---
description: >-
  Apply Cortex XSIAM Web and API Security profiles through prevention policies
  for selected workloads and workload groups.
---

# Apply Web and API Security profiles to workloads

{% hint style="info" %}
### Note

Web and API Security profiles and policies are currently a Beta feature.
{% endhint %}

Cortex XSIAM provides out-of-the-box protection for all registered workloads with a default security policy. To customize your security policy, create or edit one or more security profiles, and then attach the profiles to one or more policies.

Each policy you create must apply to one or more workload or workload groups. The **Prevention Policy Rules** table lists all the policy rules per operating system. Rules associated with one or more targets that are beyond your defined user scope are locked and cannot be edited.

1.  From Cortex XSIAM, create a policy rule.

    Do one of the following:

    *   Select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Policy Rules**, and select **+ New Policy** or **Import from File**.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When importing a policy, select whether to enable the associated policy targets. Rules within the imported policy are managed as follows:</p><ul><li>New rules are added to the top of the list.</li><li>Default rules override the default rule in the target tenant.</li><li>Rules without a defined target are disabled until the target is specified.</li></ul></div>
    * Select **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, right-click the profile that you want to assign, and click **Create a new policy rule using this profile**.
2. Enter a policy name, and a description (optional) that describes the purpose or intent of the policy.
3. Select the **Platform** for which you want to create a new policy.
4.  Select the desired profiles that you want to apply in this policy.

    If you do not specify a profile, the default profiles are used.
5. Click **Next**.
6.  Use the filters to assign the policy to one or more workloads or workload groups.

    Cortex XSIAM automatically applies the platform filter you selected and, if it exists, the **Group Name** according to the groups within your defined user scope.
7. Click **Done**.
8.  In the **Policy Rules** table, change the rule position, if needed, to order the policy relative to other policies.

    The Cortex XDR agent evaluates policies from top to bottom. When the Cortex XDR agent finds the first match, it applies that policy as the active policy. To move the rule, select the arrows and drag the policy to the desired location in the policy hierarchy.

    Right-click to display and use one of the following options **View Policy Details**, **Edit**, **Save as New**, **Disable**, and **Delete**.
9.  If you want to export policies, select one or more policies, right-click, and select **Export Policies**. You can include the associated **Policy Targets**, **Global Exceptions**, and workload groups.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The exported file is encoded in Base64 and cannot be edited.</p></div>
