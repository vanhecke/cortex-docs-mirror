# Add an integration instance

To use a downloaded integration, you must configure an integration instance.

Before you begin:

* Content packs containing integrations are downloaded when you adopt playbooks and configure playbook tasks. The content pack must be downloaded before you can configure an integration instance.
* Consider whether you want to add credentials, which enable you to save login information without exposing usernames, passwords, certificates, and SSH keys. For more information, see [Manage credentials](manage-credentials).
* Although you can view integration documentation when adding an instance, [https://xsoar.pan.dev/](https://xsoar.pan.dev/docs/reference/index) has more detailed information about integrations, including commands, outputs, and recommended permissions.

1. Navigate to **Settings** → **Data Sources & Integrations** and search for the integration for which you want to add an instance.
2. Select the integration and click **Add Instance**.
3. Add the parameters as required.
4. (Optional) To check that the integration instance is working correctly, click **Test**.
5.  **Save & Exit**.

    You can expand the integration to see more details about the integration instance, enable or disable the integration instance, and copy the instance.

    If you encounter an error, see [Troubleshoot integrations](troubleshoot-integrations).
6. By default, the integration instance is used whenever the integration is called. If you want to only use the integration instance when specified with the `using` argument in a playbook or the CLI, change the integration instance setting from **Always** to **On Demand**. For example, you might have two instances of an integration and want to use one instance as the default and the other instance only for manual testing on demand.
7. (Optional) To manage access to specific commands, see [Configure integration permissions](configure-integration-permissions).
