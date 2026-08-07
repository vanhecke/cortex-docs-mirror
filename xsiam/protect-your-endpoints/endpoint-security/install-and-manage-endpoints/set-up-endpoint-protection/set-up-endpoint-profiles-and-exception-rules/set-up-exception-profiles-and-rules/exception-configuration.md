# Exception configuration

To allow full granularity, Cortex XSIAM enables you to create exceptions from your baseline policy. With these exceptions, you can remove specific folders or paths from evaluation, or disable specific security modules. You can configure exception rules for Cortex XSIAM protection and prevention actions in a centralized location, and apply them across multiple profiles. The exceptions can be configured from **Settings** → **Exception Configuration**.

* Issue Exclusion rules specify match criteria for issues that you want to suppress.
* IOC/BIOC Suppression rules exclude one or more indicators from an IOC or BIOC rule that takes action on specific behaviors.
* Disable Injection and Prevention rules specify exceptions that bypasses a process from prevention modules and injections.
* Disable Prevention rules specify granular exceptions to prevention actions triggered for your endpoints.
* Legacy Agent Exceptions define prevention profile exception rules for all endpoints.
* Support Exception rules generate exceptions based on files provided by the support team.

Prior to Cortex XSIAM version 1.3, Legacy Agent Exceptions and Support Exceptions were configured through their relevant profiles.

Starting with version 1.3, Cortex XSIAM enables you to manage the Legacy Agent Exceptions and Support Exception configurations from a central location and easily apply them across multiple profiles in the Agent Exceptions Management page.

To manage the Prevention profile exceptions from **Exception Configuration**, you must first migrate your existing exceptions configured via profiles. Your existing exception profiles are migrated per module.

Cortex XSIAM simulates the migration to enable you to review the results before activating the migration.

### How to migrate existing exceptions

1. Select **Settings** → **Exception Configuration** → **Legacy Exceptions** and click **Start Simulation**.
2. Review the **Legacy Agent Exceptions** and the **Support Exception Rules**.
3. You can then **Activate** the new agent management page or **Cancel** to continue using the Prevention Profiles to configure individual exceptions.

{% hint style="info" %}
### Important

If you don't migrate the legacy exceptions, you can continue to create exceptions through the profiles.

* [Add a new exceptions security profile](#UUID-c186ef70-75e8-5e99-1455-89030568bcea)
* [Add a global endpoint policy exception](#UUID-7f8ab5bb-a9e1-9a16-acbf-13dfea5763bb)
* [Set up exploit prevention profiles](#UUID-6386af9a-ca64-a179-8ab8-33489f5c488c)
* [Set up malware prevention profiles](https://app.gitbook.com/s/FOhYBYLdbwpnbJgr6uaX/endpoint-security/install-and-manage-endpoints/set-up-endpoint-protection/set-up-endpoint-profiles-and-exception-rules/set-up-malware-prevention-profiles)
* [Set up restrictions prevention profiles](#UUID-782ed1ba-266a-bada-97ca-57d2dbd475e3)
{% endhint %}

After the migration, you can [Add a support exception rule](#UUID-6c5e4f51-a528-71a1-ce37-946700b6100f) or [Add a legacy exception rule](#UUID-5d26f4f4-345d-a0e7-ee52-d70e1a310a86).
