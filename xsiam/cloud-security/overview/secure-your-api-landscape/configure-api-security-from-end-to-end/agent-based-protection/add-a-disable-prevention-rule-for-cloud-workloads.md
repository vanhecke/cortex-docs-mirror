# Add a disable prevention rule for cloud workloads

You can create granular exceptions to prevention actions defined for your workloads. These exception rules may be useful when you have processes that are essential to your organization, and must not be terminated. To cover all your workloads, you can configure different exception rules per platform. Cortex Cloud still generates issues from the disabled rules.

{% hint style="info" %}
### Important

* All applicable prevention actions are skipped for the files and process that match the properties defined in the rule.
* Consider the consequences of disabling a prevention rule before you add the exception, and monitor it over time.
{% endhint %}

1. Go to **Settings** → **Exceptions Configuration** → **Disable Prevention Rules**.
2. Click **Add Rule**, and select **Web and API Security**.
3. For **Rule Name**, enter a meaningful name for the rule.
4. (Optional) Enter a description for the business reason or intent for the rule.
5. Click **Next**.
6. For **Exception Effect**, choose an option:
   * **Disable prevention and report**: Disable the prevention modules included in this rule and report on it.
   * **Disable prevention and do not report**: Disable the prevention modules included in this rule but do not report on it.
7. For **Platform**, select the operating system that you require.
8.  Under **Target Properties**, you can configure any combination of parameters. If a parameter is not specified, all values are allowed. You can use wildcards for matching. Press Enter to add the target properties. Repeat this step for additional target properties.

    When you specify two or more values, the exception is applied only if the file satisfies all the specified target properties.

    * **Domain**: Specify a domain.
    * **IP**: Specify an IP address.
    *   **User Agent**: Specify the application's User-Agent ID that is used in the headers of an API request.

        For example, if the user agent is `"User-Agent:paypal.com"`, enter `paypal.com` here.
    * **Path**: Specify the path to the required files or folders.
9.  For **Modules**, select one or more security modules that won't trigger prevention actions.

    The actions triggered by the other modules are not affected.
10. For **Scope**, select the scope for the rule:
    * If you want to apply the rule to all workloads, select **Global**.
    * If you want to apply the rule to only specific exception profiles, click **Exception Profiles**, and then select them from the list.
11. Click **Next**.
12. Review the configurations for the exception, and if the risks are acceptable to you, select **I understand the risk**, and then click **Create**.
