---
description: >-
  Learn how Cortex XSIAM case teams assign roles and control sensitive case
  access.
---

# Overview of case teams and roles

You can assign individual users and entire user groups to a case team in Cortex XSIAM. For sensitive or high-risk cases, you can restrict access to a case so that only assigned case team members can see or take action.

For more information see [Assign a case team and restrict access](../analyze-and-resolve-cases/additional-case-actions/assign-a-case-team-and-restrict-access).

## Key benefits of case teams

Assigning a case team is beneficial for:

* **Staging team assignment prior to final ownership:** Engage multiple users and user groups early in the process, allowing team members to collaborate and evaluate the case before assigning a single final owner.
* **Defining clear roles and responsibilities:** Establish clear boundaries and ownership for everyone involved in the case.
* **Restricting access to sensitive or high-risk cases:** Assign specific team members and user groups, and restrict case access so that only the defined team can view it.
* **Coordinating multi-team efforts:** Smoothly coordinate tasks when multiple distinct teams are involved in an investigation.

## Case team roles

You can assign the following roles within a case team. These roles serve as labels to indicate a team member's level of involvement and do not grant additional permissions or access.

For the Collaborator and Watcher roles, you can assign individual users or user groups.

<table><thead><tr><th width="173">Role</th><th>Description</th></tr></thead><tbody><tr><td><strong>Assignee</strong></td><td>The primary owner responsible for managing and resolving the case.</td></tr><tr><td><strong>Collaborator</strong></td><td>Team members actively assisting with specific case tasks.</td></tr><tr><td><strong>Watcher</strong></td><td>Users who need to monitor case updates but aren't directly assigned to tasks.</td></tr></tbody></table>

## Case access and visibility

You can control case visibility by adjusting a case’s **General Access** settings under **Manage case team**. By default, visibility is set to **Case Scope**.

### **Case Scope (Default)**

* **Organization-wide access:** Any user in the organization with the appropriate Scope-Based Access Control (SBAC) scope can view the case.
* **Permission requirements:** Users still require the appropriate Role-Based Access Control (RBAC) permissions to view, edit, or execute playbooks and automations.

### **Team Only**

Restricts case access exclusively to assigned team members.

* **Access Control:** Only assigned case team members can view or take action on the case.
* **Assigned team:** A case must have assigned collaborators or watchers before it can be set to **Team Only**. If a **Team Only** case has no assigned team members, its access automatically reverts to **Case Scope**.
* **Management rights:** Once a case is set to **Team Only**, only existing team members can add or remove watchers and collaborators.
* **SBAC requirements:** Team members gain full access to the case itself. However, access to underlying case data and related objects (such as issues and assets) remains strictly governed by their assigned SBAC role.
* **RBAC requirements:** Team members must still hold the necessary RBAC permissions to view, edit, or run playbooks and automations on the case.
* **Admin access rights:** Users with the **Instance Admin** and **Account Admin** roles cannot be scoped out of cases. They bypass both Case Scope and Team Only restrictions and will always have full access to all cases.
