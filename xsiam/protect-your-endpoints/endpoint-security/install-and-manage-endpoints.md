---
description: >-
  Learn how to set up profiles, policies and other settings for endpoint
  protection, how to install Cortex XDR agent on endpoints, and how to manage
  them after installation.
---

# Install and manage endpoints

Endpoint protection starts with the Cortex XDR agent that is installed on each endpoint in your environment. The agent package that you install on endpoints contains many settings that are configured by default, out-of-the-box, to enable you to get protection up and running quickly. However, these settings can also be modified and used in different combinations, by using profiles, which are then mapped to policies, and by configuring global settings.

Several endpoint management tasks can be performed remotely by administrators, from Cortex XSIAM. These include tasks such as applying tags and aliases to endpoints, upgrading the Cortex XDR agent, uninstalling and deleting the Cortex XDR agent, and more.

To stay up to date with the latest policy and endpoint status, Cortex XSIAM communicates regularly with your Cortex XDR agents. For example, when you upgrade your endpoints to the latest release, Cortex XSIAM creates an installation package and distributes it to the agent on their next communication. Similarly, the agent can send back data from the endpoint to Cortex XSIAM, such as data gathered on the endpoint or tech support files. In Cortex XSIAM, there are two types of communication.
