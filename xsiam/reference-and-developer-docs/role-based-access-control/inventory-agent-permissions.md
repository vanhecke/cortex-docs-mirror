---
description: Configure permissions for Endpoints (XDR Agent) in Cortex XSIAM.
---

# Inventory - Agent permissions

This section controls access to endpoint agent management, security policies, host firewalls, device controls, and agent lifecycles.

* [agent-administrations](inventory-agent-permissions/agent-administrations "mention")
* [agent-groups](inventory-agent-permissions/agent-groups "mention")
* [agent-prevention-policies](inventory-agent-permissions/agent-prevention-policies "mention")
* [global-exceptions](inventory-agent-permissions/global-exceptions "mention")
* [agent-profiles](inventory-agent-permissions/agent-profiles "mention")
* [agent-extension-policies](inventory-agent-permissions/agent-extension-policies "mention")
* [agent-installations](inventory-agent-permissions/agent-installations "mention")
* [host-firewall](inventory-agent-permissions/host-firewall "mention")
* [device-control](inventory-agent-permissions/device-control "mention")

{% hint style="warning" %}
### Caution

* The Master switch: Setting **Agent Administrations** to View/Edit acts as a master switch that unlocks highly granular execution checkboxes (such as Agent Management, Pause Protection, and Agent Scan). Leaving these unchecked allows the user to view the administration without the ability to execute the actions.
* High-Risk Operations:
  * Pause Protection temporarily disables malware and exploit prevention, leaving endpoints actively vulnerable to threats.
  * Token Revocation permanently disconnects agents until they are manually re-enrolled.
  * Global Exceptions bypass prevention policies and can create severe security blind spots; implement strict change management workflows
{% endhint %}
