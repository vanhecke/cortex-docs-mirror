---
description: Ingest PingFederate authentication logs into Cortex XSIAM.
---

# Ingest authentication logs from PingFederate

To receive authentication logs from PingFederate, you must first write Audit and Provisioner Audit Logs to CEF in PingFederate and then set up a Syslog Collector in Cortex XSIAM to receive the logs. After you set up log collection, Cortex XSIAM immediately begins receiving new authentication logs from the source. Cortex XSIAM creates a dataset named `ping_identity_pingfederate_raw`. Logs from PingFederate are searchable in Cortex Query Language (XQL) queries using the dataset and surfaced, when relevant, in authentication stories.

1. [Activate the Syslog Collector](../activate-syslog-collector).
2. Set up PingFederate to write logs in CEF. To set up the integration, you must have an account for the PingFederate management dashboard and access to create a subscription for SSO logs. In your PingFederate deployment, [write audit logs in CEF](https://docs.pingidentity.com/bundle/pingfederate-102/page/obk1564002980895.html). During this set up you will need the IP address and port you configured in the Syslog Collector.
3. To search for specific authentication logs or data, you can Create an Authentication Query or use the XQL Search.
