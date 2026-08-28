---
description: >-
  Use the Cortex XSIAM Threat Intel Agent to list, enrich, and update Extended
  Threat Intelligence indicators.
---

# Using XTI with Threat Intel Agent

Agentic Assistant Threat Intel (TI) Agent works with Extended Threat Intelligence (XTI) and Threat Intel Management (TIM).

* If you have XTI only enabled, the TI Agent reads from and writes to the XTI dataset. Only the actions listed below are supported.
* If you have both XTI and TIM enabled side-by-side:
  * The TI Agent reads from the XTI dataset. Only the actions listed below are supported.
  * The TI Agent writes to both XTI and TIM datasets. Only the actions listed below are supported for XTI.
* If you disable XTI, the TI Agent reads from and writes to the TIM dataset.

## TI Agent actions supported by XTI

The TI Agent can perform various read and write actions. The TI Agent can perform the following actions for XTI:

| **Action**                                                              | **Example prompt**                              |
| ----------------------------------------------------------------------- | ----------------------------------------------- |
| List indicators                                                         | Show me the most recent malicious IP indicators |
| List indicator relationships                                            | Show me relationships with 183.132.45.96        |
| Update Indicator                                                        | Update 1.1.1.10 to verdict Benign               |
| <p>Enrich Domain</p><p>Enrich File</p><p>Enrich IP</p><p>Enrich URL</p> | Show me information about 192.43.254.85         |

{% hint style="info" %}
Enrich CVE is currently not supported.
{% endhint %}

**Related links**

For general information and best practices related to enabling and using Agentic Assistant chat, see [Agentic Assistant chat](../../agentic-assistant-chat).

<br>
