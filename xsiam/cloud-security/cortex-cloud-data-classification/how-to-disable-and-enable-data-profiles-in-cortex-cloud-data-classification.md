---
description: Enable or disable data profiles in Cortex XSIAM Data Classification.
---

# How to disable and enable data profiles in Cloud Data Classification

{% hint style="info" %}
Requires a Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license. If you have the Endpoint DLP add-on, Data Classification is automatically available.
{% endhint %}

### Understand data profile statuses

Data profiles define what constitutes sensitive data for your organization and are applicable to both files and tables. You have the flexibility to enable or disable both out-of-the-box (OOTB) and custom data profiles.

* **Enabled:** When a data profile is enabled, Cortex Cloud Data Classification actively applies its definitions to identify sensitive data.
* **Disabled:** When a data profile is disabled, all data profile results are removed from the object; that is, file or table.

{% hint style="info" %}
### Note

Existing results on past scans are updated in the Asset and Object inventories within two hours after being disabled or enabled.
{% endhint %}

### Disable data profiles

You can disable data profiles that you do not require. Disabled data profiles are not searched for in new scans. Existing results on past scans are updated in the Asset and Object inventories within two hours after being disabled or enabled.

1. In the lower left part of the screen, click **Settings** → **Configurations** → **Data Classification** → **Data Profiles**.
2. Right-click the rows of the data profiles you want to disable, and in the context menu, select **Disable**.
3. In the **Disable Data Profile** screen, click **Yes** to disable the data profile or profiles that you selected, or click **No** to cancel. If you click **Yes**, the data profile will be disabled and appear grayed out. You can enable it again if required, as described below.

### Enable data profiles

You can enable data profiles after they have been disabled. Once enabled, within two hours, the profiles are recalculated on the existing data in the Asset and Object inventories. After the new scans calculate these data profiles, the results are then visible in all relevant modules.

1. Right-click the rows of the disabled data profiles that you want to enable, and in the context menu, click **Enable**.
2. In the **Enable Data Profile** screen, click **Yes** to enable the data profile or profiles that you selected, or click **No** to cancel.

{% hint style="info" %}
### Note

For more information about data profiles in Cortex Cloud Data Classification, see [What is Cortex Cloud Data Classification?]().
{% endhint %}

### Important considerations

* **Global impact of built-in data profiles**: You can only enable or disable them.
* **Flexibility for custom profiles:** You can do the following with custom data profiles, including those you have duplicated from built-in data profiles:
  * Edit
  * Duplicate
  * Delete
  * Disable
  * Enable
