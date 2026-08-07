---
description: Configure permissions for Endpoints (XDR Agent).
---

# Inventory - Agent permissions

This section controls access to endpoint agent management, security policies, host firewalls, device controls, and agent lifecycles.

{% hint style="warning" %}
### Caution

* The Master switch: Setting **Agent Administrations** to View/Edit acts as a master switch that unlocks highly granular execution checkboxes (such as Agent Management, Pause Protection, and Agent Scan). Leaving these unchecked allows the user to view the administration without the ability to execute the actions.
* High-Risk Operations:
  * Pause Protection temporarily disables malware and exploit prevention, leaving endpoints actively vulnerable to threats.
  * Token Revocation permanently disconnects agents until they are manually re-enrolled.
  * Global Exceptions bypass prevention policies and can create severe security blind spots; implement strict change management workflows
{% endhint %}
