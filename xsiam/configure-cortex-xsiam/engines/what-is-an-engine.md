---
description: >-
  Learn what a Cortex XSIAM engine is and how it securely runs integrations and
  automation.
---

# What is an engine?

An engine is a proxy server application that is installed on a remote machine and enables communication between the remote machine and the Cortex XSIAM tenant. You can run playbooks, scripts, commands, and integrations on the remote machine, and the results are returned to the tenant.

While the Cortex XSIAM tenant includes a user interface that allows security analysts to create and manage playbooks, investigate issues, and perform other tasks, the engine operates behind the scenes to execute these playbooks and automate security actions. The separation between the user interface and the engine allows for the scalable and efficient execution of security automation and orchestration.

You can install multiple engines on the same machine (Shell installation only), which is useful in a dev-prod environment where you do not want to have numerous engines in different environments and to manage those machines.

{% hint style="info" %}
You cannot share a multiple-engine installation with a single-engine installation.
{% endhint %}

**Engine architecture**

![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-b0304600f73006f80c2e99e3266f11d356895c91%2F84bc2be2aebb0f69603b3215944bb0d9664960968d414a30076debc2f2c15079.png?alt=media)

Within the network, you need to allow the engine to access the Cortex XSIAM’s IP address and listening port (by default, TCP 443). The engine always initiates the communication to Cortex XSIAM.

**Engine use cases**

An engine can be used for the following purposes:

*   **Engine proxy**

    Cortex XSIAM engines enable you to access internal or external services that are otherwise blocked by a firewall or a proxy. For example, if a firewall blocks external communication and you want to run the Rasterize integration, you need to install an engine to access the Internet.
*   **Engine load-balancing**

    Engines can be part of a load-balancing group, which enables the distribution of the command execution load. The load-balancing group uses an algorithm to efficiently share the workload for integrations that the group is assigned to, thereby speeding up execution time. In general, heavy workloads are caused by playbooks that run multiple commands.

    ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f08131928591f5eafd11ab9c3691edaf283986de%2F1c15df2690151d8158e098cca908083274a97a58c2c6a6bad91bbca61a67ce9c.png?alt=media)

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>When you add an engine to a load-balancing group, you cannot use that engine separately. The engine does not appear in the engines menu when configuring an integration instance, but you can choose the load-balancing group.</p></div>
