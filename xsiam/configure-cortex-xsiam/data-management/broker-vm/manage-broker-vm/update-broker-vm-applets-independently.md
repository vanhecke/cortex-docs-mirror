---
description: Update Cortex XSIAM Broker VM applets independently.
---

# Update Broker VM applets independently

Cortex XSIAM allows you to update individual Broker VM applets independently. This enables faster deployment of hot-fixes and new features with minimal broker downtime.

### Applet versioning and visibility

You can view the current version of an active applet by navigating to **Settings** > **Configurations** > **Data Broker** > **Broker VMs** and clicking the applet icon in the **APPS** column.

### Automatic applet updates

If **Auto Upgrade** is enabled for your Broker VM, applets will upgrade automatically when a new version is available.

* For standalone brokers: The applet updates as soon as a new version is available.
* For clusters: Applets follow a rolling upgrade mechanism to ensure service continuity.

### Manual applet updates

When a new version of an applet is released, Cortex XSIAM triggers a notification:

1. The applet status indicator changes to orange, indicating a **WARNING** state.
2. A message appears in the applet hovering menu: **New version available: X.Y.Z**.
3. To update, select **Update** from the hovering menu.
4. While the update is in progress, the status displays as Updating.
5. Upon completion, the status indicator changes to green, indicating a **CONNECTED** state.
6. A successful update is recorded in the **Management Audit Logs**.

<br>
