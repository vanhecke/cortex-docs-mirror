# Add a disable injection and prevention rule

You can generate a temporary exception to bypass a process from prevention modules and injections. You can specify paths, or command line, from both prevention and injection. This may be useful when you have processes that are essential to your organization and must not be terminated. Cortex XSIAM still generates issues from data collections.

{% hint style="info" %}
### Important

* Exceptions are limited up to 48 hours by default and configurable up to one week.
* Consider the consequences of disabling a prevention rule before you add the exception and monitor it over time.
* You can only apply a Disable Prevention Rule to agents version 7.9 and later.
{% endhint %}

1. Select **Settings** → **Exception Configuration** → **Disable Injection and Prevention**.
2. Click **+Add Injection Rule**.
3. Specify a rule name and an optional description.
4. Select the platform. To cover all your endpoints, you can prevent different exception rules per platform.
5. Add the **Process Name** , and specify the **Path** to bypass.
6. Select the time limit for the exception rule.
7. Select the **Scope** for the rule. If you want to apply the rule to only specific **Exception Profiles**, select them from the list.
8. Enable the rule.
9. Click **Yes**, to confirm that you acknowledge that the selected rules will be disabled.
