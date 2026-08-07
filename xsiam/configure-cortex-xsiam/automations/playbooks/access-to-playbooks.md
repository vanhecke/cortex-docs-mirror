# Access to playbooks

Access to playbooks is managed at the object level, enforcing least-privileged access for automation logic. This ensures that sensitive workflows, such as remediation playbooks or custom playbooks, are only visible to and editable by authorized users. For a complete description of how object-level access affects playbook visibility across Cortex XSIAM, see [Manage access to playbooks and scripts](../../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management).

**Playbook access roles**

When a playbook is shared, users are assigned one of the following levels:

* **Owner**: Full control over the object and its permissions.
* **Editor**: Can view and modify the playbook definition and logic.
* **Viewer**: Can view the playbook structure and use it in workflows but cannot make changes.
