---
description: >-
  Configure Cortex XSIAM Email Remediation Response Rules to automate responses
  to email threats.
---

# Email Remediation Response Rules

View all remediation rules that apply to email threats, create new rules and modify them to customize them to your needs.

The Email Remediation Response Rules page is under **Modules** → **Email Security** → **Remediation** → **Rules** and displays the following widgets and the Rules table.

### Remediation Rules widgets

The widgets on this page summarize and give insights into which rules have been activated and applied.

* **Rule Status**: Overview of email rule statuses, Enabled or Disabled.
* **Rule Actions**: Actions taken as a result of the rules applied.
* **Rule Hits**: Breakdown of the number of rules that were applied.

### Remediation Rules table

The table displays all email remediation response rules for your organization. The rules are applied in the order listed in the table. The higher the rule in the table, the more priority it has. If an email triggers a rule, the rest of the rules below it in the table aren't triggered for the same email.

You can change the priority ranking of a rule by dragging the rule to the desired location in the table.

Use the right click menu on any row to Disable Rule, Edit, Save as New, Delete rule and to copy the entire row.

#### Create an Email Remediation Response Rule

Create a remediation rule that will be applied automatically to all received emails that meet the conditions of the rule.

1. In **Modules** → **Email Security** → **Remediation** → **Rules**, click **Create Rule**.
2. Type a rule name and a description.
3.  Select the actions to be taken. You can select one or more.

    * Soft delete email: places the email in the Deleted Items folder.
    * Tag as phishing: sends the marked email to a designated Phishing folder.
    * Send warning email: sends an email with descriptions of the actions taken.
    * Move email to folder: moves the email to a designated folder.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>For automated actions not yet supported by the response engine, use the playbooks, scripts, and commands in the Cortex XSIAM automation engine. For more information, see <a href="../../../configure-cortex-xsiam/automations/automation-in-cortex-xsiam">Automation in Cortex XSIAM</a>.</p></div>
4. Change the rule activation toggle as necessary. The default is **Enable Rule**.
5. Click **Next**.
6. Select to which users to apply the rule.
   * **All Users:** Select if you want to apply the rule to all the organization, except for a few specific users or groups who you want to exclude.
   * **Users Selection:** Select if you want to apply the rule to specific users. From the Users list that opens, configure your selection in one of the following ways:
     * Static list made up of specific users you select.
     * Dynamic list automatically updated based on a filter you define. If the rule is defined for people in a certain group in the organization, and there's a change in the group, the rule will apply only to the current members of that group.
7. **Exclude Users** from this rule if you don't want the rule to apply to them. You can exclude specific people or apply a filter to exclude users with shared details.
8. Review the **Users Preview** and make any changes you want.
9. Select a Quick Template from our recommended templates or define your own conditions from scratch.

#### Quick Template:

The conditions for the rule are displayed. You can use the template as it is or customize it by changing the predefined conditions or adding new conditions.

{% hint style="info" %}
### Note

If you apply a new template, all the customizations to the previous template you used will be lost.
{% endhint %}

| Template name                     | Description                                                                                        | Condition details                                                                                                                            |
| --------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Malicious URL Detected            | Automatically remediates emails containing URLs classified as malicious by Advanced URL Filtering. | <p>Detection Method = AURL</p><p>Alert Name = "AURL - Email contains URL(s) classified as malicious"</p><p>Severity &#x26;amp;gt; Medium</p> |
| Malicious Attachment Identified   | Triggers remediation for emails with attachments identified as malicious by WildFire.              | <p>Detection Method = SaaS Attachments</p><p>Alert Name = "WildFire Malware"</p><p>Severity > Medium</p>                                     |
| SPF & DMARC Failures              | Removes spoofed emails failing both SPF and DMARC validation.                                      | <p>Alert Name contains "Suspicious SPF Result" or</p><p>"Suspicious DKIM Result" or</p><p>"Suspicious DMARC result"</p>                      |
| Non-corporate Cloud Sharing Links | Detects suspicious links to file-sharing services not commonly used by your organization.          | Alert Name contains "External email with file-sharing link" AND Severity >= LOW                                                              |
| Suspicious URL Categories         | Targets emails linking to risky web content such as gambling or adult content.                     | urls.primary\_category intersects \['gambling', 'adult-and-pornography']                                                                     |

#### Define Conditions:

Use the filters detailed in the following table to define rule conditions. This option provides an exceptional degree of granularity to customize your rule conditions.

| Attribute                      | Type           | Condition example                                                       |
| ------------------------------ | -------------- | ----------------------------------------------------------------------- |
| Alert Name                     | String         |                                                                         |
| Severity                       | enum           | High/Medium/Low                                                         |
| Detection type                 | enum           | Detection type = WF/ AURL/Analytics                                     |
| day\_of\_week                  | enum           | day\_of\_week in \['Sat','Sun']                                         |
| sender\_ip                     | IP             | sender\_ip not\_in\_cidr \['10.0.0.0/8','192.168.0.0/16']               |
| sender\_ip\_geo.country        | String         | sender\_ip\_geo.country not\_in \['US','IL','GB']                       |
| spf.result                     | enum           | spf.result in \['fail','softfail']                                      |
| dmarc.result                   | enum           | dmarc.result == 'fail'                                                  |
| body.language                  | Set (string)   | body.language == 'en'                                                   |
| urls.count                     | Number         | urls.count >= 3                                                         |
| urls.any\_malicious            | Boolean        | urls.any\_malicious == true                                             |
| urls.primary\_category         | enum           | urls.primary\_category intersects \['gambling','adult-and-pornography'] |
| urls.risk\_level               | Set (string)   | urls.risk\_level intersects \['high-risk']                              |
| attachments.count              | Number         | attachments.count >= 1                                                  |
| attachments.extensions         | Set (string)   | attachments.extensions intersects \['exe','js','hta']                   |
| attachments.total\_size        | Number (bytes) | attachments.total\_size > 1000000                                       |
| headers.has\_list\_unsubscribe | Boolean        | headers.has\_list\_unsubscribe == true                                  |
| headers.auto\_submitted        | enum           | headers.auto\_submitted in \['auto-replied','auto-generated']           |
| headers.reply\_to              | String         | domain(headers.reply\_to) != domain(from.address)                       |

10. Click **Next**.
11. Review the rule summary and either go back to change them or click **Create**.
12. In the rules table, to configure the priority of the rule drag it to its place and click **Save**. You can only save the rule after you have configured its priority.
