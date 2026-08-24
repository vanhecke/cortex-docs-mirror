---
description: >-
  Create and manage Cortex XSIAM policies that exclude critical assets from
  automated remediation.
---

# Manage automation exclusion policies

Automation exclusion policies prevent commands and scripts from performing automated remediation actions on critical assets, such as users, IP addresses, and domains. For example, a playbook task might block multiple domains, but mission-critical domains in the policy list would not be blocked.

Admin users and all roles with read/write permissions to the Automation Exclusion Center can edit, disable, and enable policies.

1. Go to **Settings** → **Configurations** → **Automation** → **Automation Exclusion Center**.
2. Right-click on a policy and choose **Edit**.
3. From the **Edit Policy** page, you can do the following:
   * Enable or disable the policy. Policies are enabled by default.
   * Enable or disable policy overrides. If you enable policy overrides, users can manually run the commands and scripts on the excluded critical assets, using the `override-policy` parameter. Use of the `override-policy` parameter is included in the Management Audit Logs.
   *   Select one or more lists of excluded assets.

       Clicking the list icon opens a new browser tab for the **Lists** page, where you can create and edit lists.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>For the <strong>IAM User Hard Remediation</strong> and <strong>User Soft Remediation</strong> policies, we recommend including username, email, and ID for each user you want to exclude. Example: <code>username1, user@example.com, userID112</code>.</p></div>

       Each list can be filtered by conditions, such as `Equals`, `Ends with`, and `Doesn't include`. For example, you can exclude all email addresses with your company's domain using the `Ends with` filter.
   * For **IAM User Hard Remediation** and **User Soft Remediation** policies, you can also select asset groups. These policies can include only lists, only asset groups, or a combination of asset groups and lists.
   * Under **THEN skip execution of the following commands and scripts**, click to view the scripts and commands affected by the policy. Commands only appear if they are part of an active integration instance. You cannot edit the list of scripts and commands.
4. **Save** your changes.

{% hint style="info" %}
### Note

You can also right click on a policy from the main **Automation Exclusion Center** page to disable or enable the policy.

If you click on a list name in the **Exclude** column, that list opens in the **Lists** page.
{% endhint %}
