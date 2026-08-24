---
description: Ingest Cisco ASA and AnyConnect logs into Cortex XSIAM.
---

# Ingest logs from Cisco ASA firewalls and AnyConnect

If you use Cisco ASA firewalls or Cisco AnyConnect VPN, you can take advantage of Cortex XSIAM investigation and detection capabilities by forwarding your firewall and AnyConnect VPN logs to Cortex XSIAM. This enables Cortex XSIAM to examine your network traffic to detect anomalous behavior. Cortex XSIAM can use Cisco ASA firewall logs and AnyConnect VPN logs as the sole data source, but can also use Cisco ASA firewall logs in conjunction with Palo Alto Networks firewall logs. For additional endpoint context, you can also use Cortex XSIAM to collect and alert on endpoint data.

When Cortex XSIAM starts to receive logs, the app can begin stitching network connection logs with other logs to form network stories. Cortex XSIAM can also analyze your logs to generate Analytics issues, and can apply IOC, BIOC, and Correlation Rules matching. You can also use queries to search your network connection logs using the Cisco Cortex Query Language (XQL) dataset (`cisco_asa_raw`).

To integrate your logs, you first need to set up an applet in a Broker VM within your network to act as a Syslog Collector. You then configure forwarding on your log devices to send logs to the Syslog Collector in a CISCO format.

1. Verify that your Cisco ASA firewall and Cisco AnyConnect VPN logs meet the following requirements.

* Syslog in Cisco-ASA format
* Must include `timestamps`
* Only supports the following messages.
  * For Cisco ASA firewall: 302013, 302014, 302015, 302016
  * For Cisco AnyConnect VPN: 113039, 716001, 722022, 722033, 722034, 722051, 722055, 722053, 113019, 716002, 722023, 722037

2. [Activate the Syslog Collector](../activate-syslog-collector).
3. Increase log storage for Cisco ASA firewall and Cisco AnyConnect VPN logs. As an estimate for initial sizing, note that the average Cisco ASA log size is roughly 180 bytes. For proper sizing calculations, test the log sizes and log rates produced by your Cisco ASA firewalls and Cisco AnyConnect VPN logs. For more information, see Manage Your Log Storage within Cortex XSIAM.
4. Configure the Cisco ASA firewall and Cisco AnyConnect VPN, or the log devices forwarding logs from Cisco, to log to the Syslog Collector in a CISCO format.\
   Configure your firewall and AnyConnect VPN policies to log all traffic and forward the traffic logs to the Syslog Collector in a CISCO format. By logging all traffic, you enable Cortex XSIAM to detect anomalous behavior from Cisco ASA firewall logs and Cisco AnyConnect VPN logs. For more information on setting up Log Forwarding on Cisco ASA firewalls or Cisco AnyConnect VPN, see the Cisco ASA Series documentation.
