---
description: >-
  An overview of user notifications for the Cortex XDR agent during
  installation, upgrade, and removal on a Mac.
---

# Manage the Agent Deployment Notifications for Mac

When you install, upgrade, or remove the Cortex XDR agent from your Mac endpoint, both the operating system and the Cortex XDR agent prompt specific notifications the end user has to approve. The operating system notifications are in line with Apple’s security improvements that started from macOS 10.15.4, which included the deprecation of kernel extensions by third-party providers. As a result, Cortex XDR agent 7.1 and later releases no longer use the kernel extension. Instead, the agent is designed to deploy two System Extensions.

Since the 7.1 release, the Cortex XDR agent deploys the Endpoint Security extension to monitor system events, and since the 7.2.1 agent release, a Network extension was added to monitor network events. Together, these two System extensions provide full coverage of the endpoint traffic and replace the deprecated kernel extension. To suppress the extension notifications for the Cortex XDR agent installation process, refer to [Install the Cortex XDR Agent Using JAMF](install-the-cortex-xdr-agent-for-mac/install-the-cortex-xdr-agent-using-jamf). For a one-click installation using a MDM of your choice, refer to [Install with a Unified Configuration Profile for MDMs](install-the-cortex-xdr-agent-for-mac/install-with-a-unified-configuration-profile-for-mdms).

The following tables describe the extension and notification approval workflow the end user is required to perform on a Mac endpoint during agent installation, upgrade, and removal processes.

#### Installing a Cortex XDR Agent

The following table describes the extension approval workflow the end user is required to perform on the endpoint during agent installation, when performed manually or using an MDM.

|                            | macOS 10.15.4 and later                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Install a Cortex XDR agent | <ul><li><strong>Endpoint Security extension</strong>—Requires user approval. Can be suppressed in your MDM profile.</li><li><strong>Network extension</strong>—Requires user approval. Can be suppressed in your MDM profile.</li><li><strong>Network content filter</strong>—Requires user approval. Can be suppressed in your MDM profile. You can also suppress this operating system prompt by uploading a configuration file provided by Palo Alto Networks.</li></ul> |

#### Upgrading a Cortex XDR Agent

The following table describes the extension approval workflow the end user is required to perform on the endpoint during agent upgrade, when performed manually or using an MDM.

|                            | macOS 10.15.4 and later                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Upgrade a Cortex XDR agent | <ul><li><strong>Endpoint Security extension</strong>—If already allowed during initial agent installation, nothing to allow during upgrade. Otherwise, allow once. Can be suppressed in your MDM profile.</li><li><strong>Network extension</strong>—If already allowed during initial agent installation, nothing to allow during upgrade. Otherwise, allow once. Can be suppressed in your MDM profile.</li><li><strong>Network content filter</strong>— If you are using an MDM to deploy the agents in your networks, you can suppress this operating system prompt by uploading a configuration file provided by Palo Alto Networks. Otherwise, if you are upgrading from a 7.2.1 agent or later and approval was already provided, nothing to allow during upgrade.</li></ul> |

#### Removing a Cortex XDR Agent

The following table describes the approval workflow the end user is required to perform on the endpoint during agent removal, when performed manually or using an MDM.

|                           | macOS 10.15.4 and later                                                                                                                                                                                                            |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Remove a Cortex XDR agent | <ul><li>User approval and password are required by Apple for each System extension. In the current operating system release, you cannot suppress this option in your MDM profile, and will be required to approve twice.</li></ul> |
