---
description: Enable or disable data patterns in Cortex XSIAM Data Classification.
---

# How to disable and enable data patterns in Data Classification

{% hint style="info" %}
Requires a Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license. If you have the Endpoint DLP add-on, Data Classification is automatically available.
{% endhint %}

### Disable data patterns

You can disable data patterns that you do not require. Disabled data patterns are not searched for in new scans. Existing results on past scans do not change.

{% hint style="info" %}
### Note

Disabling data patterns can cause changes in your data profile results and stop detection of these data patterns.
{% endhint %}

1. In the lower left part of the screen, click **Settings** → **Configurations** → **Data Classification** → **Data Patterns**.
2. Right-click the rows of the data patterns you want to disable, and in the context menu, select **Disable**.
3. In the **Disable Data Pattern** screen, click **Yes** to disable the data pattern or patterns that you selected, or click **No** to cancel. If you click **Yes**, the data pattern will be disabled and appear grayed out. You can enable it again if required, as described below.

### Enable data patterns

You can enable data patterns after they have been disabled. Once enabled, new scans classify these data patterns and the results are then visible in all relevant modules.

1. Right-click the rows of the disabled data patterns that you want to enable, and in the context menu, click **Enable**.
2. In the **Enable Data Pattern** screen, click **Yes** to enable the data pattern or patterns that you selected, or click **No** to cancel.

{% hint style="info" %}
### Note

For more information about data patterns in data classification, see [What is Cortex Cloud Data Classification?]().
{% endhint %}
