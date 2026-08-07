# XDR Collectors

{% hint style="info" %}
Ingestion of log events larger than 5 MB is not supported.
{% endhint %}

Cortex XSIAM provides an XDR Collectors (XDRC) configuration that is dedicated for on-premise data collection on Windows and Linux machines. The XDRC includes a dedicated installer, a collector upgrade configuration, content updates, and policy management. The XDRC is a data collector that gathers and processes logs and events from multiple sources. It leverages Elasticsearch Filebeat, a lightweight log shipper, to collect log data from various systems and applications. Additionally, Winlogbeat gathers Windows event logs, ensuring comprehensive visibility into Windows environments. These components facilitate centralized analysis, threat detection, and investigation across the Cortex XSIAM ecosystem.
