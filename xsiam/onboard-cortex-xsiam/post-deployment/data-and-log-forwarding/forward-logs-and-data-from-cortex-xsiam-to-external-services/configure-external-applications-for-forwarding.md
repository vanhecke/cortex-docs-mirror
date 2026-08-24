---
description: >-
  Configure external applications in Cortex XSIAM to forward cases, issues, and
  logs to email, Slack, syslog, Amazon S3, Amazon SQS, Splunk, and webhooks.
---

# Configure external applications for forwarding

Cases, issues, and logs can be forwarded to third-party external services. The external service must be configured in Cortex XSIAM before you set up notification forwarding.

Only cases and issues can be forwarded to Slack, Amazon S3, Amazon SQS, Splunk, and Webhook. Before forwarding cases or issues to Splunk, Amazon S3, Amazon SQS, or Webhook, you need to configure egress in the Cortex Gateway.

You do not need to configure egress for email, Slack, or syslog forwarding. No prior configuration is required to send data or logs to an email distribution list.

{% hint style="info" %}
### Note

You can configure external applications using either of these methods:

* Pre-configuration: Navigate to **Settings → Configurations → Integrations → External Applications** and follow the setup guide for your specific service:
  * [forward-notifications-to-amazon-sqs](configure-external-applications-for-forwarding/forward-notifications-to-amazon-sqs "mention")
  * [forward-notifications-to-amazon-s3](configure-external-applications-for-forwarding/forward-notifications-to-amazon-s3 "mention")
  * [forward-notifications-to-splunk](configure-external-applications-for-forwarding/forward-notifications-to-splunk "mention")
  * [forward-notifications-to-webhook](configure-external-applications-for-forwarding/forward-notifications-to-webhook "mention")
  * [integrate-a-syslog-receiver](configure-external-applications-for-forwarding/integrate-a-syslog-receiver "mention")
  * [integrate-slack-for-outbound-notifications](configure-external-applications-for-forwarding/integrate-slack-for-outbound-notifications "mention")
* In-workflow configuration: Navigate to **Settings → Configurations → General → Notifications → Add Forwarding Notifications**. Define the configuration and notification scope, then click **Add Application** and complete the setup steps for your chosen service.
{% endhint %}
