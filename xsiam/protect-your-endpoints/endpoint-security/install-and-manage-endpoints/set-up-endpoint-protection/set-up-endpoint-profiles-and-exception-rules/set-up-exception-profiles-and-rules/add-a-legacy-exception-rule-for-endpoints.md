---
description: >-
  Add Cortex XSIAM legacy exception rules for endpoint compatibility
  requirements.
---

# Add a legacy exception rule for endpoints

Legacy Exception rules enable you to configure an exception to prevention and protection modules on endpoints for selected profiles.

Items included in allow lists may continue to generate Cortex XSIAM security events. If you want to exclude event reporting, configure this on the **Issue Exclusions** page (**Settings** → **Exception Configurations** → **Issue Exclusions**).

Keep in mind the following:

* Prior to Cortex XSIAM version 1.3, legacy exceptions were configured through profiles.
* Starting with version 1.3, Cortex XSIAM enables you to manage the malware security exceptions from a central location and easily apply them across multiple profiles in the **Legacy Agent Exceptions Management** page.

To manage the prevention profile exceptions from **Exception Configuration**, you must first migrate your existing exceptions configured via the prevention profiles.

Your migrated rules are displayed on the **Settings** → **Exception Configurations** → **Legacy Agent Exceptions** page. For more information about the migration, see [Exception configuration](exception-configuration).

1. Select **Settings** → **Exception Configurations** → **Legacy Agent Exceptions**, and then click **+ Add Rule**.
2. Select the platform for which you want to create an agent exception.
3. Select the module for which you want to create an exception. Optionally, select **Select all** to apply the exception to all profiles for this module or select specific profiles.
4. For each module, enter the file or folder path that you want to add to the exception rule, and press ENTER. Repeat this step to add additional paths to the rule.
5. Select the endpoint profiles to which you want to apply this rule.
6. Click **Next**.
7. Review the rule, and then select the warning message checkbox.
8. Click **Create**.

{% hint style="info" %}
### Important

If you don't migrate the legacy exceptions, you can continue to create exceptions through the profiles.

* [Add a new exceptions security profile](add-a-legacy-exception-rule-for-endpoints/add-a-new-exceptions-security-profile)
* [Add a global endpoint policy exception](add-a-legacy-exception-rule-for-endpoints/add-a-global-endpoint-policy-exception)
* [Set up exploit prevention profiles](../set-up-exploit-prevention-profiles)
* [Set up malware prevention profiles](../set-up-malware-prevention-profiles)
* [Set up restrictions prevention profiles](../set-up-restrictions-prevention-profiles)
{% endhint %}
