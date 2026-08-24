---
description: Ingest Forcepoint DLP logs into Cortex XSIAM.
---

# Ingest logs from Forcepoint DLP

If you use Forcepoint DLP to prevent data loss over endpoint channels, you can take advantage of Cortex XSIAM investigation and detection capabilities by forwarding your logs to Cortex XSIAM. This enables Cortex XSIAM to help you expand visibility into data violation by users and hosts in the organization, correlate and detect DLP incidents, and query Forcepoint DLP logs using XQL Search.

When Cortex XSIAM starts to receive logs, Cortex XSIAM can analyze your logs in XQL Search and you can create new Correlation Rules.

To integrate your logs, you first need to set up an applet in a Broker VM within your network to act as a Syslog Collector. You then configure forwarding on your log devices to send logs to the Syslog Collector in a CEF or LEEF format.

Configure Forcepoint DLP collection in Cortex XSIAM.

1. Verify that your Forcepoint DLP meet the following requirements.

* Must use version 8.8.0.347 or a later release.
* On premise installation only.

2. [Activate the Syslog Collector](../activate-syslog-collector) applet on a Broker VM in your network. Ensure the Broker VM is configured with the following settings.

* Format: Select either a CEF or LEEF Syslog format.
* Vendor: Specify the Vendor as `forcepoint`.
* Product: Specify the Product as `dlp_endpoint`.

3. Increase log storage for Forcepoint DLP logs. As an estimate for initial sizing, note the average Forcepoint DLP log size. For proper sizing calculations, test the log sizes and log rates produced by your Forcepoint DLP. For more information, see Manage Your Log Storage.
4. Configure the log device that receives Forcepoint DLP logs to forward syslog events to the Syslog Collector in a CEF or LEEF format. For more information, see the [Forcepoint DLP documentation](https://help.forcepoint.com/emailsec/en-us/on-prem/8.5.x/email_siem/guid-bde9b920-e7cb-4845-a1ac-4742ff2aeb1d.html).
5. After Cortex XSIAM begins receiving data from Forcepoint DLP, you can use XQL Search to search your logs using the `forcepoint_dlp_endpoint` dataset.
