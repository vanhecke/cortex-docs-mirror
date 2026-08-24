---
description: Ingest Check Point firewall logs into Cortex XSIAM.
---

# Ingest logs from Check Point firewalls

If you use Check Point FW1/VPN1 firewalls, you can still take advantage of Cortex XSIAM investigation and detection capabilities by forwarding your Check Point firewall logs to Cortex XSIAM. Check Point firewall logs can be used as the sole data source, however, you can also use Check Point firewall logs in conjunction with Palo Alto Networks firewall logs and additional data sources.

Cortex XSIAM can stitch data from Check Point firewalls with other logs to make up network stories searchable in the Query Builder and in Cortex Query Language (XQL) queries. Cortex XSIAM can also return raw data from Check Point firewalls in XQL queries.

{% hint style="info" %}
* Logs with `sessionid = 0` are dropped.
* Destination Port data is available only in the raw logs
{% endhint %}

In terms of alerts, Cortex XSIAM can both surface native Check Point firewall alerts and generate its own issues on network activity. Issues are displayed throughout Cortex XSIAM issue, case, and investigation views.

To integrate your logs, you first need to set up an applet in a Broker VM within your network to act as a Syslog Collector. You then configure your Check Point firewall policy to log all traffic and set up the Log Exporter on your Check Point Log Server to forward logs to the Syslog Collector in a CEF format.

When Cortex XSIAM starts to receive logs, the app can begin stitching network connection logs with other logs to form network stories. Cortex XSIAM can also analyze your logs to generate Analytics issues, and can apply IOC, BIOC, and Correlation Rule matching. You can also use queries to search your network connection logs.

1. Ensure that your Check Point firewalls meet the following requirements. Check Point software version: R77.30, R80.10, R80.20, R80.30, or R80.40
2. Increase log storage for Check Point firewall logs. As an estimate for initial sizing, note that the average Check Point log size is roughly 700 bytes. For proper sizing calculations, test the log sizes and log rates produced by your Check Point firewalls. For more information, see Manage Your Log Storage within Cortex XSIAM.
3. [Activate the Syslog Collector](../activate-syslog-collector).
4. Configure the Check Point firewall to forward Syslog events in CEF format to the Syslog Collector. Configure your firewall policy to log all traffic and set up the Log Exporter to forward logs to the Syslog Collector. For more information on setting up Log Exporter, see the Check Point documentation.
