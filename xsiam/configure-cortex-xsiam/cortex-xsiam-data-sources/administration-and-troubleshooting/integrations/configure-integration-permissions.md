# Configure integration permissions

You can use role-based access control (RBAC) to restrict running commands to specific roles at the integration instance level. If you have multiple instances of the same integration, you can assign different roles (permission levels) for the same command in each instance.

For example, you may want limit the roles that can run potentially harmful commands, such as the ability to isolate endpoints.

Users who do not have permission to run a command cannot do the following:

* Run the command from the CLI.
* Complete pending tasks in a Work Plan that uses the restricted command.
* Edit arguments for playbook tasks that use the restricted command.
* Select the command when editing a playbook.
* Leverage the restricted command when executing a reputation command, such as IP, Domain, and File.

If you have multiple instances of the same integration, you can assign different roles (permission levels) for the same command in each instance.

To view or edit integration permissions:

1.  Go to Settings → **Configurations** → Data Collection → **Integration Permissions**.

    You can see a list of all enabled integrations.
2.  Select the integration.

    You can see the following:

    * **INSTANCE:** Lists all instances for the integration.
    * **COMMANDS:** Lists all commands for the integration.
    * **PERMITTED ROLES:** Lists the roles that have permission to run the command. Default is **No Restrictions**.
3. For a specific command, restrict the roles that can run the command.
   1. Go to the relevant command.
   2. Click **Edit**.
   3. In the **PERMITTED ROLES**, column, select the roles that you want to allow running the command.
4. Save the integration permissions.
