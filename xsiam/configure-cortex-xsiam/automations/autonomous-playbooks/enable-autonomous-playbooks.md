# Enable autonomous playbooks

When the Autonomous Playbooks feature is enabled, new, fully managed incident response content is installed.

{% hint style="info" %}
This feature is enabled by default for all new tenants created on or after May 31st, 2026. If you would like to add this feature to an existing tenant, contact Customer Support.

To enable or disable the Autonomous Playbooks feature, you must be an Account Admin or Instance Administrator.
{% endhint %}

To enable Autonomous Playbooks, go to **Settings** → **Configurations** → **Automation** → **Autonomous Playbooks**. After reviewing the information about autonomous playbooks, you have the option to either **Replace deprecated content** (replace the existing content pack) or to **Keep deprecated and new content**. After making your selection, click **Enable**.

We recommend replacing the deprecated content. If you choose to keep the deprecated content, you will see duplicate playbooks and automation rules. You can then manually delete or disable the deprecated content.

After you enable the Autonomous Playbooks feature, you can view a list of all integrations included in the autonomous playbooks. You can filter this list by integration name, configuration status: **Configured**, **Not configured yet**, **Dismissed**, or by category such as **Investigation** or **Data Collection**.

For non-configured integrations, you can right click on the integration name to configure or dismiss. We recommend dismissing integrations that are not relevant for your organization. For example, a playbook might include two options to create tickets in an external system and only one option is relevant for your organization.

{% hint style="info" %}
To disable the Autonomous Playbooks feature, go to **Settings** → **Configurations** → **Automation** → **Autonomous Playbooks**, click the three dot more options icon in the upper right-hand corner, and select **Disable Autonomous Playbooks**.

If you disable the Autonomous Playbooks feature, all autonomous playbooks and automation rules are disabled and removed from the system and are no longer visible in the Playbooks or Automation Rules page.

If you enable the Autonomous Playbooks feature again after disabling it, any autonomous automation rules you manually disabled previously will be active and you will need to manually disable them again on the Automation Rules page. If you previously moved the autonomous automation rules block, it will return to the top of the automation rules list.

If you disable the Automation Playbooks feature, there is an option to provide feedback on your experience.
{% endhint %}
