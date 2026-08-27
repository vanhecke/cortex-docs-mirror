---
description: Cortex XSIAM steps for adding a playbook to a content pack.
---

# Add a Playbook to a Content Pack

Use the `demisto-sdk download --item-type Playbook -i "PLAYBOOK NAME"` to add a playbook to a content pack.

Playbook triggers should be added to the content pack Triggers folder.

{% hint style="info" %}
Currently, Cortex XSIAM does not support exporting playbook triggers into the Content repo unless you turn on a feature flag.
{% endhint %}
