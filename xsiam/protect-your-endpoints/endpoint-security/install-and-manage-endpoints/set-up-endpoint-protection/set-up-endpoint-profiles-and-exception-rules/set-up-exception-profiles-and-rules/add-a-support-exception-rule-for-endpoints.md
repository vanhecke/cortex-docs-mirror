# Add a support exception rule for endpoints

You can define and manage exceptions based on files received from the customer support team. You can apply the rule across all of your endpoints or to specific profiles.

Keep in mind the following:

* Prior to Cortex XSIAM version 1.3, support exceptions were configured through profiles.
* Starting with version 1.3, Cortex XSIAM enables you to manage the support exceptions from a central location and easily apply them across multiple profiles on the **Support Exception Rules** page.

To manage the prevention profile exceptions from **Exception Configuration**, you must first migrate your existing exceptions configured via the Prevention profiles.

Your migrated rules are displayed on the **Settings** → **Exception Configurations** → **Support Exception Rules** page. For more information about the migration, see [Exception configuration](exception-configuration).

1. From **Settings** → **Exception Configuration** → **Support Exception Rules**, click **+ Import from file**.
2. Locate the JSON file you received from the customer support team.
3. Select to apply the rule to specific **Profiles** or select **Global** to apply to all endpoints.

{% hint style="info" %}
### Important

If you don't migrate the legacy exceptions, you can continue to create exceptions through the profiles.

* [Add a new exceptions security profile](add-a-legacy-exception-rule-for-endpoints/add-a-new-exceptions-security-profile)
* [Add a global endpoint policy exception](add-a-legacy-exception-rule-for-endpoints/add-a-global-endpoint-policy-exception)
* [Set up exploit prevention profiles](../set-up-exploit-prevention-profiles)
* [Set up malware prevention profiles](../set-up-malware-prevention-profiles)
* [Set up restrictions prevention profiles](../set-up-restrictions-prevention-profiles)
{% endhint %}
