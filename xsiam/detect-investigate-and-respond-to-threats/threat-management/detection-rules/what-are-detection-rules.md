---
description: >-
  Explore Cortex XSIAM IOC, BIOC, and correlation rules for detecting threats
  and generating issues.
---

# What are detection rules?

Cortex XSIAM uses rules to detect threats in your network and to generate issues. You can add specific detection rules for which you want Cortex XSIAM to generate issues. The following are the different types of rules available:

* **Indicators of compromise (IOCs)**: IOCs are used to alert for known artifacts that are considered malicious or suspicious. IOCs are static, simple, and based on the detection of criteria such as SHA256 hashes, IP addresses and domains, file names, and paths. You create IOC rules based on information you gather from various threat-intelligence feeds or as a result of an investigation within Cortex XSIAM. For example, if you find out that a certain ransomware uses a certain file hash, you can add the file hash as an IOC and generate an issue if it is detected.
* **Behavioral indicators of compromise (BIOCs)**: BIOCs detect suspicious behavior. As you identify specific activities (network, process, file, registry, etc) that indicate a threat, you create BIOCs that can alert you when the behavior is detected. If you enable **Cortex XSIAM Analytics**, Cortex XSIAM can use [Analytics BIOCs](../analytics/analytics-overview/analytics-issues-and-analytics-biocs) (ABIOCs) to establish baseline behavior and detect any deviation from this behavior.
* **Correlation Rules**: Correlation rules help you analyze the relationship between multiple events from multiple sources by using the Cortex Query Language (XQL) based engine.
