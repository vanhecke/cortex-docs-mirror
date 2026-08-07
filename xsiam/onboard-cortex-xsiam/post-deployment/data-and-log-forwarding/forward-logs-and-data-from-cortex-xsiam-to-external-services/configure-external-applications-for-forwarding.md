# Configure external applications for forwarding

Cases, issues, and logs can be forwarded to third-party external services. The external service must be configured in Cortex XSIAM before you set up notification forwarding.

Only cases and issues can be forwarded to Slack, Amazon S3, Amazon SQS, Splunk, and Webhook. Before forwarding cases or issues to Splunk, Amazon S3, Amazon SQS, or Webhook, you need to configure egress in the Cortex Gateway.

You do not need to configure egress for email, Slack, or syslog forwarding. No prior configuration is required to send data or logs to an email distribution list.

{% hint style="info" %}
### Note

There are two options for configuring external applications. To configure relevant external applications before you begin creating forwarding notifications, follow the steps in the following topics using the menu path **Settings** → **Configurations** → **Integrations** → **External Applications**. You can also configure an external application as part of the workflow for configuring notification forwarding found at **Settings** → **Configurations** → **General** → **Notifications** → **Add Forwarding Notifications**. After defining the configuration and setting the scope of the notifications, you can select an existing external application or **Add Application**. After you choose **Add Application**, the steps are identical to those described in the following topics.
{% endhint %}
