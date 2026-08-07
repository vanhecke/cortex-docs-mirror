# Playbook examples

## Assign case team and restrict case to Team only

This playbook automatically fetches high-severity cases, retrieves system groups, assigns a dedicated team of watchers and contributors, and restricts access to ensure a secure investigation.

{% stepper %}
{% step %}
**Task 1: Get high severity cases**

Retrieves all open cases flagged as high severity.

* **Script:** `getCases (Builtin)`
* **Parameters:**

| Parameter key | Value  | Description                           |
| ------------- | ------ | ------------------------------------- |
| `severities`  | `high` | Filters for high-severity cases only. |
{% endstep %}

{% step %}
**Task 2: Get system groups**

Retrieves all user groups in the system.

* **Script:** `getSystemGroups (Builtin)`
* **Parameters:** _This task does not require any input parameters._
{% endstep %}

{% step %}
**Task 3: Assign watchers to cases**

Assigns specific user groups to the case team of the retrieved cases and sets the watcher role.

* **Script:** `setCase (Builtin)`
* **Parameters:**

| Parameter key            | Value / Source                                                                  | Description                                                             |
| ------------------------ | ------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `case_ids`               | `${Core.Case.case_id}`                                                          | Target case IDs from the playbook context (Task 1).                     |
| `case_team_ids`          | `Get Core.SystemGroup.groupId Where Core.SystemGroup.groupName Equals SOCteam1` | Dynamically selects the group ID for the system group named "SOCteam1". |
| `case_team_member_types` | `user_group`                                                                    | Defines the member type as a user group.                                |
| `case_team_roles`        | `watcher`                                                                       | Sets the team role type to watcher.                                     |
| `case_team_operation`    | `add`                                                                           | Adds the selected user group to the case team.                          |
{% endstep %}

{% step %}
**Task 4: Assign contributors to cases**

Assigns specific users to the case team of the retrieved cases and sets the contributor role.

* **Script:** `setCase (Builtin)`
* **Parameters:**

| Parameter key            | Value / Source                           | Description                                              |
| ------------------------ | ---------------------------------------- | -------------------------------------------------------- |
| `case_ids`               | `${Core.Case.case_id}`                   | Target case IDs from the playbook context (Task 1).      |
| `case_team_ids`          | `<User1@example.com><User2@example.com>` | Explicitly selects specific target user email addresses. |
| `case_team_member_types` | `user`                                   | Defines the member type as an individual user.           |
| `case_team_roles`        | `contributor`                            | Sets the team role type to contributor.                  |
| `case_team_operation`    | `add`                                    | Adds the selected users to the case team.                |
{% endstep %}

{% step %}
**Task 5: Restrict case access**

Changes the case access scope to Team Only, which restricts access solely to the assigned case team (assignee, contributor, or watcher roles).

{% hint style="warning" %}
This task must always come _after_ defining the case team and roles. You cannot set a case to "Team Only" if no case team has been assigned yet.
{% endhint %}

* **Script:** `setCase (Builtin)`
* **Parameters:**

| Parameter key | Value                  | Description                                              |
| ------------- | ---------------------- | -------------------------------------------------------- |
| `case_ids`    | `${Core.Case.case_id}` | Target case IDs from the playbook context (Task 1).      |
| `access_mode` | `team_only`            | Restricts visibility strictly to the assigned case team. |
{% endstep %}
{% endstepper %}

***

## Remove users and user groups assigned to the case team

This playbook purges context data and removes any existing users or user groups from the assigned case team for high severity cases.

{% stepper %}
{% step %}
**Task 1: Delete context**

Deletes all existing context data from the case.

* **Script:** `DeleteContext`
* **Parameters:**

| Parameter key | Value | Description                                      |
| ------------- | ----- | ------------------------------------------------ |
| `all`         | `yes` | Deletes all existing context data from the case. |
{% endstep %}

{% step %}
**Task 2: Get high severity cases**

Retrieves all open cases flagged as high severity.

* **Script:** `getCases (Builtin)`
* **Parameters:**

| Parameter key | Value  | Description                           |
| ------------- | ------ | ------------------------------------- |
| `severities`  | `high` | Filters for high-severity cases only. |
{% endstep %}

{% step %}
**Task 3: Check if group team exists**

A conditional task that checks whether any case team is currently assigned to the retrieved cases.

* **Type:** Built-in condition
* **Conditional paths:**

| Path | Condition criteria                      | Description                                               |
| ---- | --------------------------------------- | --------------------------------------------------------- |
| Yes  | `${Core.Case.caseTeam.id}` is not empty | Routes to Task 4 if a case team ID exists.                |
| Else | `${Core.Case.caseTeam.id}` is empty     | Routes to the end of the playbook if no team is assigned. |
{% endstep %}

{% step %}
**Task 4: Clean case team**

Removes all user and user group data from the selected case team fields for the target cases. This task runs only if Task 3 resolves to "Yes". After this task completes, the playbook concludes automatically.

* **Script:** `setCase (Builtin)`
* **Parameters:**

| Parameter key            | Value / Source                     | Description                                                             |
| ------------------------ | ---------------------------------- | ----------------------------------------------------------------------- |
| `case_ids`               | `${Core.Case.case_id}`             | Target case ID from the playbook context.                               |
| `case_team_ids`          | `${Core.Case.caseTeam.id}`         | Selects the active case team IDs found in the context.                  |
| `case_team_member_types` | `${Core.Case.caseTeam.memberType}` | Targets all assigned member types (both users and user groups).         |
| `case_team_roles`        | `${Core.Case.caseTeam.teamRole}`   | Targets all active team roles (contributors and watchers).              |
| `case_team_operation`    | `remove`                           | Completely removes the selected users, groups, and roles from the case. |
{% endstep %}
{% endstepper %}
