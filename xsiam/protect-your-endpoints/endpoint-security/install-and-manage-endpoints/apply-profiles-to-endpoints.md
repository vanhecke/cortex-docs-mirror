---
description: Apply Cortex XSIAM profiles to endpoints using targeted policy rules.
---

# Apply profiles to endpoints

Cortex XSIAM provides out-of-the-box protection for all registered endpoints with a default security policy customized for each supported platform type. To customize your security policy, create or edit one or more security profiles, and then attach the profiles to a new or existing policy.

Each policy you create must apply to one or more endpoints or endpoint groups. The Prevention Policy Rules table lists all the policy rules per operating system. Rules associated with one or more targets that are beyond your defined user scope are locked and cannot be edited.

{% stepper %}
{% step %}
From Cortex XSIAM, create a policy rule.

Do one of the following:

*   Select Inventory → Endpoints → Policy Management → Prevention → Policy Rules, and select + New Policy or Import from File.

    When importing a policy, select whether to enable the associated policy targets. Rules within the imported policy are managed as follows:

    * New rules are added to the top of the list.
    * Default rules override the default rule in the target tenant.
    * Rules without a defined target are disabled until the target is specified.
* Select Inventory → Endpoints → Policy Management → Prevention → Profiles, right-click the profile you want to assign and click Create a new policy rule using this profile.
{% endstep %}

{% step %}
Define a Policy Name and optional Description that describes the purpose or intent of the policy.
{% endstep %}

{% step %}
Select the Platform for which you want to create a new policy.
{% endstep %}

{% step %}
Select the desired Exploit, Malware, Restrictions, and Agent Settings profiles you want to apply in this policy.

If you do not specify a profile, the Cortex XDR agent uses the default profile.
{% endstep %}

{% step %}
Click Next.
{% endstep %}

{% step %}
Use the filters to assign the policy to one or more endpoints or endpoint groups.

Cortex XSIAM automatically applies the platform filter you selected and, if it exists, the Group Name according to the groups within your defined user scope.
{% endstep %}

{% step %}
Click Done.
{% endstep %}

{% step %}
In the Policy Rules table, change the rule position, if needed, to order the policy relative to other policies.

The Cortex XDR agent evaluates policies from top to bottom. When the Cortex XDR agent finds the first match it applies that policy as the active policy. To move the rule, select the arrows and drag the policy to the desired location in the policy hierarchy.

Right-click to select one of the following options: View Policy Details, Edit, Save as New, Disable, and Delete.
{% endstep %}

{% step %}
If you want to export policies, select one or more policies, right-click and select Export Policies. You can include the associated Policy Targets, Global Exceptions, and endpoint groups.

The exported file is encoded in Base64 and cannot be edited.
{% endstep %}
{% endstepper %}
