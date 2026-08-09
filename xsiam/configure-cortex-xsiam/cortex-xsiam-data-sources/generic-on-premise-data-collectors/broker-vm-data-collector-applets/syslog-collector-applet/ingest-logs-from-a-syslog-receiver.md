---
description: >-
  To extend visibility, Cortex XSIAM can receive Syslog from additional vendors
  that use CEF or LEEF formatted over Syslog (TLS not supported).
---

# Ingest logs from a Syslog receiver

Cortex XSIAM can receive Syslog from a variety of supported vendors (see [Syslog Collector applet]()). In addition, Cortex XSIAM can receive Syslog from additional vendors that use CEF, LEEF, CISCO, CORELIGHT, or RAW formatted over Syslog.External data ingestion vendor support

After Cortex XSIAM begins receiving logs from the third-party source, Cortex XSIAM automatically parses the logs in CEF, LEEF, CISCO, CORELIGHT, or RAW format and creates a dataset with the name `<vendor>_<product>_raw`. You can then use XQL Search queries to view logs and create new IOC, BIOC, and Correlation Rules.

To receive Syslog from an external source:

1. Set up your Syslog receiver to forward logs.
2. Activate the Syslog collector applet on a Broker VM within your network. For more information, see [Activate the Syslog Collector](activate-syslog-collector).
3. Use the XQL Search to search your logs.
