# Create a case

{% hint style="info" %}
### Note

To create a case manually, you must have View/Edit permission for **Cases and Issues** selected under **Settings** → **Configurations** → **Access Management** → **Roles** → **Components** → **Cases & Issues**.
{% endhint %}

You can create a case directly from the **Cases** page.

1. On the **Cases** page click **New Case**.
2.  Under **Case Details**, specify the case domain, name, severity, and (Optional) assignee and description.

    The severity of a manually generated case cannot be low.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can assign a case to a single domain only, and you cannot change the assigned domain. For more information, see <a href="../../overview-of-cases/case-and-issue-domains">Case and issue domains</a>.</p></div>
3.  (Optional) Under **Case Fields**, select custom case fields.

    Cortex XSIAM validates the **Host IP**, **Local IP**, and **Remote IP** fields.

    If you select **Set fields as default for new \<domain> domain cases**, the custom case fields that are configured are saved for all users. When a user next creates a case for the same domain, these fields are automatically configured instead of the default field set.

    To reset the custom fields to the system default, click **Restore Default Field Set**.
4.  Under **Issue Details**, select the issues to link to the case, or create a new issue.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>The issues that you link to a case can be linked to multiple cases, and the issue domains do not need to match the case domain.</p></div>
5.  Under **Issue Fields**, define the following:

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>This option is only relevant for certain domains.</p></div>

    * MITRE ATT\&CK tactics and techniques to assign to the case.
    * Custom issue fields.
6.  (Optional) Under **Playbook**, specify playbook run settings. By default, a playbook is run **Automatically by trigger**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>This option is only relevant for certain domains.</p></div>
7.  Click **Create new case**.

    Each case creation generates one issue. The name, the severity, and the description of the generated issue mirrors the name, the severity, and the description of the case.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can't attach files to manually created cases.</p></div>
