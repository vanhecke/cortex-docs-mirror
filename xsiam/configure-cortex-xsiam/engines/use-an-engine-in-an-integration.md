---
description: >-
  Use an engine or a load-balancing group of engines to fetch issues and run
  commands for an integration.
---

# Use an engine in an integration

When you create an integration instance, you can select whether to fetch issues and run commands executed for the integration using the engine or a load-balancing group of engines. After you add the engine or load-balancing group to an integration instance, you can run commands using the engine or load-balancing group by specifying the **`using`** argument in the Issues War Room.

Before configuring an integration to run using multiple engines in a load-balancing group, we recommend that you test the integration using a single engine in the load-balancing group.

{% hint style="info" %}
Long-running integrations should not run on load-balancing groups.
{% endhint %}

**Command Example**

**`!url url="www.cnn.com" using=urlscan.io_instance_1`**
