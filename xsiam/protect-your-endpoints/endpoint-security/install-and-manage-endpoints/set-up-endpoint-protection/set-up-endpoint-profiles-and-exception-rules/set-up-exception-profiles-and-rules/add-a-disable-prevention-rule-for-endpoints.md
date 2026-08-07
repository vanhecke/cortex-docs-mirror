# Add a disable prevention rule for endpoints

You can create granular exceptions to prevention actions defined for your endpoints. In your disable prevention rules, you can specify hash types, file/folder paths, signers, certificate thumbprint, command line, or processes to exclude from the prevention actions triggered by specific security modules. These rules may be useful when you have processes that are essential to your organization, and must not be terminated. To cover all your endpoints, you can configure different exception rules per platform. Cortex XSIAM still generates issues from the disabled rules.

{% hint style="info" %}
### Important

* All applicable prevention actions are skipped for the files and process that match the properties defined in the rule.
* Consider the consequences of disabling a prevention rule before you add the exception, and monitor it over time.
* You can only apply a Disable Prevention Rule to endpoints running Cortex XDR agents version 7.9 and later.
{% endhint %}

1. Go to **Settings** → **Exception Configuration** → **Disable Prevention Rules**.
2. Click **+Add Rule**.
3. For **Rule Name**, enter a meaningful name for the rule.
4. (Optional) Enter a description for the business reason or intent for the rule.
5. Click **Next**.
6. For **Platform**, select the operating system that you require.
7.  Under **Target Properties**, you can configure any combination of parameters. If a parameter is not specified, all values are allowed.

    When you specify two or more values, the exception is applied only if the file satisfies all the specified target properties.

    You can use wildcards for matching the **Command Line** or **Files/Folders** path.

    * **Hash:** enter a specific SHA256 hash
    * **Files/Folders:** specify the path to the required files or folders
    * **Command Line:** specify a command line argument
    * **Signer Name:** specify a trusted signer
    * **Certificate Thumbprint:** specify a certificate thumbprint
8.  For **Modules**, select one or more security modules that won't trigger prevention actions.

    The actions triggered by the other modules are not affected.
9. For **Scope**, select the scope for the rule:
   * If you want to apply the rule to all endpoints, select **Global (all endpoints)**.
   * If you want to apply the rule to only specific exception profiles, click **Exception Profiles**, and then select them from the list.
10. Click **Next**.
11. Review the configurations for the exception, and if the risks are acceptable to you, select **I understand the risk**, and then click **Create**.
