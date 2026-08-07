---
description: Export threat indicators for use in external systems and workflows.
---

# Export indicators

In the Indicators table, you can export indicators in a CSV or STIX file. You can also export indicators using an integration or a playbook.

<details>

<summary>Export indicators using the Generic Export Indicators Integration</summary>

You can export indicators in a hosted text file (External Dynamic list) from Cortex XSIAM or an engine using the Generic Export Indicators Service integration. Exported indicators can be used for example in firewall block lists, allow lists, and monitoring and analysis in Splunk. See [Generic Export Indicators Service](https://xsoar.pan.dev/docs/reference/integrations/edl).

The Generic Export Indicators Service integration can be configured to export specific fields in different output formats. Multiple instances of the integration can be configured for different indicator queries, and the output can be customized to work with a variety of third-party services.

You can set up the Generic Export Indicators Service integration by setting up a long-running integration. See [Forward Requests to Long-Running Integrations](../../../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting/integrations/forward-requests-to-long-running-integrations).

If you configure the Generic Export Indicator to run on-demand, use the `!export-indicators-list-update` command for the first time to initialize the export process.

</details>

<details>

<summary>Export indicators using playbooks</summary>

Cortex XSIAM provides out-of-the-box playbooks for TIM, including playbooks that enable you to export indicators. All TIM-related playbooks have the 'TIM' prefix. Some are generic and some are dedicated to a specific vendor, like QRadar (for example, [TIM - QRadar Add Domain Indicators](https://xsoar.pan.dev/docs/reference/playbooks/tim---q-radar-add-domain-indicators)) and ArcSight (for example, [TIM- Arcsight Add IP Indicators](https://xsoar.pan.dev/docs/reference/playbooks/tim---arc-sight-add-ip-indicators)).

If you define a playbook task input that pulls from indicators, the entire playbook runs in Quiet Mode. This means the task or playbook information is not written to the War Room, and inputs and outputs are not displayed in the playbook. However, errors and warnings are still written to the War Room.

{% hint style="warning" %}
### Caution

You should not run a query on a field that you might change in the playbook flow. For example, you shouldn’t have a playbook with query **`Verdict:Malicious`** and then change the indicator verdict as a part of the playbook.
{% endhint %}

</details>
