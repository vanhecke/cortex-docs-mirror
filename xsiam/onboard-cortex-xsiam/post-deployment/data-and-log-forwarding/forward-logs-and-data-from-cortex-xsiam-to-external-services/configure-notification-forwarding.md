---
description: >-
  Configure Cortex XSIAM forwarding notifications for issues, cases, and audit
  logs with scoped filters, formats, grouping, and external destinations.
---

# Configure notification forwarding

After you integrate with an external service such as Slack, a syslog server, Amazon S3, Amazon SQS, Webhook, or Splunk, create a forwarding configuration that specifies the data or log type you want to forward. You can configure notifications for issues, cases, and logs. To send reports to email or Slack, see Run or schedule reports.

{% hint style="warning" %}
### Prerequisite

Before you can select an external service for notification forwarding, you must integrate the external service with Cortex XSIAM. For more information, see [Configure external applications for forwarding](configure-external-applications-for-forwarding). No prior configuration is required to send data to an email distribution list.
{% endhint %}

How to configure notifications

1. Select Settings → **Configurations** → **General** → **Notifications** → **Add Forwarding Configuration**.
2. Enter a name for the configuration.
3.  Select the data or log type you want to forward:

    *   **Issues:** Send notifications for specific issue types.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li><strong>Forwarding destinations</strong>: Only issues and cases can be forwarded to Slack, Splunk, Amazon SQS, Amazon S3, or Webhook.</li><li><strong>Notification forwarding by domain</strong>: To configure notification forwarding for issues by domain, select <strong>Issues</strong> and filter the Issues table by <strong>Issue Domain</strong>.</li><li><p><strong>Alert vs. issue format</strong>: By default, new configurations use the issue format, but you can select the alert format if needed when forwarding to email, Slack, or a syslog server. You cannot forward issues in the alert format to Splunk, Amazon SQS, Amazon S3, or Webhook.</p><p>Existing legacy configurations are not automatically updated and continue to send notifications in the alert format. To use the issue format, edit the existing configuration.</p></li></ul></div>
    * **Agent Audit Logs:** Send notifications for audit logs reported by your Cortex XDR agents.
    * **Management Audit Logs:** Send notifications for audit logs about events related to your Cortex XSIAM tenant.
    * **Cases:** Send notifications for specific cases.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Not all data and log types can be sent to all external services. For more information, see <a href="">Forward logs and data from Cortex XSIAM to external services</a>.</p></div>
4. (Optional) Enter a description of the forwarding configuration.
5.  Click **Next**, and under **Scope**, filter which issues, cases, or logs you want included in a notification.

    For example, for a filter set to `Severity = Medium, Category = Configuration`, Cortex XSIAM sends the issues or events matching this filter as a notification.
6. Click **Next**.
7. Select email or the external service you want to forward to.

<details>

<summary>Email (Issues, cases, logs)</summary>

1. Enable the email option and click **Email** to expand the form.
2. Enter the email address for your **Distribution List**.
3. For issue forwarding, you can define the **Grouping Timeframe**, which is the time frame, in minutes, to specify how often Cortex XSIAM sends notifications. Every 20 issues aggregated within this time frame are sent together in one notification, sorted according to severity. To send a notification when one issue is generated, set the time frame to **`0`**. The grouping time frame for case and management audit log is 10 minutes and cannot be modified.
4. (Optional) Define your email configuration:
   1. In the **Distribution List**, add the email addresses to which you want to send email notifications.
   2. Choose whether you want Cortex XSIAM to provide an auto-generated subject.
   3. Choose the format you want to send the email. If you choose **Alert**, you can choose the **Standard** or **Legacy** format. For more information about the legacy format, see [Log format for IOC and BIOC issues](../data-and-log-notification-formats/log-format-for-ioc-and-bioc-issues).
5. Choose whether you want Cortex XSIAM to provide an auto-generated subject or enter your own subject.
6. By default, data is sent in the issue format. You can also choose **Alert** format, **Standard** or **Legacy**. For more information about the legacy format, see [Log format for IOC and BIOC issues](../data-and-log-notification-formats/log-format-for-ioc-and-bioc-issues).

{% hint style="info" %}
The **Grouping Timeframe** defines the time frame, in minutes, of how often Cortex XSIAM sends notifications. Every 20 issues or 20 events aggregated within this time frame are sent together in one notification, sorted according to severity. To send a notification when one issue or event is generated, set the time frame to **`0`**.
{% endhint %}

</details>

<details>

<summary>Syslog server (Issues, logs)</summary>

1. Enable the Syslog option and click **Syslog** to expand the form.
2. Select a syslog receiver. Cortex XSIAM displays the list of receivers integrated with your Cortex XSIAM tenant.
3. Choose the format you want to send the syslog. If you choose **Alert**, you can choose the **Standard** or **Legacy** format. For more information about the legacy format, see [Log format for IOC and BIOC issues](../data-and-log-notification-formats/log-format-for-ioc-and-bioc-issues).

</details>

<details>

<summary>Slack (Issues, cases)</summary>

1. Enable the Slack option and click **Slack** to expand the form.
2. Enter the Slack channel name and select from the list of available channels. Slack channels are managed independently of Cortex XSIAM in your Slack workspace. After integrating your Slack account with your Cortex XSIAM tenant, Cortex XSIAM displays a list of specific Slack channels associated with the integrated Slack workspace.
3. Choose the format you want to send the syslog. If you choose **Alert**, you can choose the **Standard** or **Legacy** format. For more information about the legacy format, see [Log format for IOC and BIOC issues](../data-and-log-notification-formats/log-format-for-ioc-and-bioc-issues).

</details>

<details>

<summary>Amazon S3, Amazon SQS, Splunk, or Webhook (Issues, cases)</summary>

1. Enable the Amazon S3, Amazon SQS, Splunk, or Webhook option and click to expand the form.
2. Select the instance name.

</details>

8. Click **Next**.
9. Review the forwarding configuration and click **Create**.
