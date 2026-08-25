---
description: >-
  Learn how Cortex XSIAM assigns case and issue domains to organize response
  work.
---

# Case and issue domains

Depending on the objects identified in a case or issue, each case and issue is assigned to a domain that reflects the root cause and the system areas of operation.

Domains are a contextual boundary that allow you to manage and prioritize each use case and help you to differentiate between your security use cases and non-security use cases. Domains help you to organize and manage your work efforts, streamline the assignment of cases, and enable you to create tailored experiences for each domain.

When an issue is created, Cortex XSIAM automatically assigns it to a domain, and the same domain is assigned to the associated case. If you create your own case, you can select the domain to which you want to assign it.

Each case and issue is assigned to a single domain. You cannot change the assigned domain, however cases can be linked to issues from different domains.

### **Built-in domains**

Cortex XSIAM provides the following built-in domains:

<table><thead><tr><th width="116.5">Domain</th><th>Description</th></tr></thead><tbody><tr><td>Security</td><td><p>For cases and issues that are associated with case response activities for detecting, preventing, and blocking threats as they occur in runtime.</p><p>For example, the identification of malware in a file, a compromised endpoint, or a phishing attempt. These cases can be assigned to a SOC analyst who specializes in blocking and remediating attacks.</p></td></tr><tr><td>Posture</td><td><p>For cases and issues that are associated with risk management activities to detect and mitigate risks to assets in the environment before they occur in runtime, and improve resilience.</p><p>For example, misconfigurations in cloud instances, over-permissive users, or the detection of secrets or shadow data. These cases can be assigned to an analyst who specializes in strengthening the security posture.</p><p>The Posture domain has subcategories that define the posture issue (Configurations, Vulnerability, Identity, etc).</p></td></tr><tr><td>Health</td><td>For cases and issues that are associated with health monitoring activities, to ensure optimal platform performance and gain insights into health drifts. For example, disruptions in data ingestion, collector connectivity errors, correlation rule errors, and event forwarding errors.</td></tr><tr><td>Hunting</td><td>For cases and issues that are associated with identifying and mitigating potential security threats before they cause any damage. For example, monitoring network traffic, analyzing logs, and conducting vulnerability assessments.</td></tr><tr><td>IT</td><td>For cases and issues that are associated with operational activities for ensuring availability and reliability in system performance. For example, server outages, network connectivity issues, application performance problems, or IT tasks.</td></tr></tbody></table>

{% hint style="info" %}
### Note

You can create your own custom domains to match specific scenarios in your environment. For more information, see [Create a case domain](../../../configure-cortex-xsiam/customize-cases-and-issues/create-a-case-domain).
{% endhint %}
