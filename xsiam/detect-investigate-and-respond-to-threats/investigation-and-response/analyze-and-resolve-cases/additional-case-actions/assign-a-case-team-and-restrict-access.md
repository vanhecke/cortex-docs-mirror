# Assign a case team and restrict access

You can assign individual users and entire user groups to specific roles within a case team. For sensitive or high-risk cases, you can also restrict access to a case so that only assigned case team members can see or take action.

For more information about the different team roles, see [Overview of case teams and roles](../../overview-of-cases/overview-of-case-teams-and-roles).

{% hint style="warning" %}
To change the access settings of a case, you must have the **Restrict Case Access** permission under **Cases & Issues**.
{% endhint %}

### How to assign a case team and restrict access

{% stepper %}
{% step %}
#### **Select the main case assignee**

Click the assignee icon and select a user.

{% hint style="info" %}
This is the primary owner responsible for managing and resolving the case.
{% endhint %}
{% endstep %}

{% step %}
#### **Define the case team**

1. Click **Manage case team**.
2. Add users or user groups, and select their specific roles (Collaborator or Watcher).
{% endstep %}

{% step %}
#### **Restrict case access**

Under **General access**, select **Team Only**.

{% hint style="info" %}
Restricting case access limits visibility exclusively to the main case assignee and any users or user groups assigned to the case team as **Collaborator** or **Watcher**.
{% endhint %}
{% endstep %}

{% step %}
#### **Save your changes**
{% endstep %}
{% endstepper %}

#### Alternative methods

You can also run this process using these alternative methods:

* **Agentic Assistant:** Use natural language prompts in the Agentic Assistant to assign a user or user group to roles in the team, and restrict case access.
* **Playbooks:** Create a playbook task that assigns team members and changes the default case scope. For more information, see [Playbook examples](assign-a-case-team-and-restrict-access/playbook-examples).
* **API:** Run the **setCase** command with the following arguments:

<details>

<summary>setCase arguments</summary>

For more detailed information about using these arguments, see [setCase](https://app.gitbook.com/s/BRTpZOj0R6io0DhO3abn/case-commands).

| `case_team_operation`    | Add, replace, or remove team members                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `case_team_ids`          | Specify users (email) or user groups (UUID)                                                                                                                                                                                                                                                                                                                                              |
| `case_team_member_types` | Define the team member type (Individual user or user group)                                                                                                                                                                                                                                                                                                                              |
| `case_team_roles`        | Set the team member role (contributor or watcher)                                                                                                                                                                                                                                                                                                                                        |
| `access_mode`            | <p>Set case visibility:</p><ul><li><code>CASE_SCOPE</code>: (default) any user whose scope permits can view the case.</li><li><code>TEAM_ONLY</code>: restricts access to team members only.</li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>You cannot set a case to <code>TEAM_ONLY</code> if no case team has been assigned.</p></div> |

</details>

### Important considerations

Before restricting access or assigning teams, keep the following rules in mind:

* **Permissions required:** To change the access settings of a case, you must have the **Restrict Case Access** permission under **Cases & Issues**.
* **Team management:** When case access is restricted to **Team Only**, only assigned team members have permission to add new team members to the case. For more information see [Overview of case teams and roles](../../overview-of-cases/overview-of-case-teams-and-roles).
* **Automatic reversion:** If a case has no assigned team members, the scope automatically reverts to **Case Scope**.
* **Audit trail:** Any changes made to the case assignee or the case team are permanently recorded in the **Case Timeline**.

