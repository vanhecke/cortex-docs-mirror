---
description: >-
  Forward Cortex XSIAM logs, cases, and issues to email, Slack, syslog, Splunk,
  Amazon SQS, Amazon S3, or webhooks.
---

# Forward logs and data from Cortex XSIAM to external services

You can forward logs, cases, and issues from Cortex XSIAM to an external service. By forwarding logs and data, you can manage alerts and investigations in external systems and meet data retention requirements. Available services include the following:

* **Slack channel and/or syslog receiver:** Configure the external application with Cortex XSIAM. After the application is configured, configure notification forwarding, specifying the data/log type you want to forward.
* **Email distribution list:** Configure notification forwarding, specifying the data/log type you want to forward.
* **Splunk, Amazon SQS, Amazon S3, and Webhook:** Only cases and issues can be forwarded to these services. The external application must be configured in Cortex XSIAM and egress configured in the Cortex Gateway before forwarding to these services.

The following table shows the log types supported for each notification type:

| Data/log type                                                | Email | Slack | Syslog | Splunk, Amazon SQS, Amazon S3, Webhook |
| ------------------------------------------------------------ | ----- | ----- | ------ | -------------------------------------- |
| Issues                                                       | ✓     | ✓     | ✓      | ✓                                      |
| Cases                                                        | ✓     | ✓     | —      | ✓                                      |
| <p>Agent Audit Logs</p><p>Note:<br>Requires an XDR Agent</p> | ✓     | —     | ✓      | —                                      |
| Management Audit Logs                                        | ✓     | —     | ✓      | —                                      |
| Health Issues (Deprecated)                                   | ✓     | ✓     | ✓      | —                                      |
