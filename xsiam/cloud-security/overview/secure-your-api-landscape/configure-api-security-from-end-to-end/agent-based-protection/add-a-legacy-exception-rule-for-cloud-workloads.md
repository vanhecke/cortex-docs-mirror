# Add a legacy exception rule for cloud workloads

Legacy Exception rules enable you to configure an exception to prevention and protection modules on workloads for selected profiles.

Items included in allow lists may continue to generate Cortex Cloud security events. If you want to exclude event reporting, configure this on the **Issue Exclusions** page (**Settings** → **Exception Configurations** → **Issue Exclusions**).

1. Select **Cases & Issues** → **Issues**.
2. Locate an issue from which you can create an exception rule, and right-click it.
3. Select **Manage Issue** → **Create Issue Exception**.
4. Select the items that you want to be included in the exception rule:
   * **Domain**: The domain to be excluded by the rule. For example, google.com
   * **Path**: The path to files or folders to be excluded by the rule.
   * **User-Agent**: The application's User-Agent ID to be excluded by the rule. For example, a User-Agent ID for the curl application could be `curl/7.68.0`
   * **IP address**: The IP address to be excluded by the rule.
5. Select an option for **Exception Scope**:
   * **Global**: Apply the exception rule globally for all workloads.
   * **Profile**: Apply the rule only to workloads mapped to the profile selected in the next step.
6. If you selected **Profile**, select a profile from the **Exception Profile Name** list.
7.  Click **Create**.

    Your rule is created, and can be viewed at the following location: **Settings** → **Exceptions Configuration** → **Legacy Agent Exceptions**.
