---
description: Collect Microsoft Azure Event Hub data with Cortex XSIAM.
---

# Ingest logs from Microsoft Azure Event Hub

Cortex XSIAM can ingest different types of data from **Microsoft Azure Event Hub** using the Microsoft Azure Event Hub data collector. To receive logs from Azure Event Hub, you must configure the settings in Cortex XSIAM based on your Microsoft Azure Event Hub configuration. After you set up data collection, Cortex XSIAM begins receiving new logs and data from the source.

When Cortex XSIAM begins receiving logs, the app creates a new dataset (`MSFT_Azure_raw`) that you can use to initiate XQL Search queries. For example, queries refer to the in-app XQL Library. For enhanced cloud protection, you can also configure Cortex XSIAM to normalize Azure Event Hub audit logs, including Azure Kubernetes Service (AKS) audit logs, with other Cortex XSIAM authentication stories across all cloud providers using the same format, which you can query with XQL Search using the `cloud_audit_logs` dataset. For logs that you do not configure Cortex XSIAM to normalize, you can change the default dataset. Cortex XSIAM can also generate Cortex XSIAM issues (Analytics, IOC, BIOC, and Correlation Rules) when relevant from Azure Event Hub logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only raised on normalized logs.

Enhanced cloud protection provides:

* Normalization of cloud logs
* Cloud logs stitching
* Enrichment with cloud data
* Detection based on cloud analytics
* Cloud-tailored investigations

{% hint style="warning" %}
**Warning**

* Misconfiguration of Event Hub resources could cause ingestion delays.
* In an existing Event Hub integration, do not change the mapping to a different Event Hub.
* Do not use the same Event Hub for more than two purposes.
{% endhint %}

The following table provides a brief description of the different types of Azure audit logs you can collect.

{% hint style="info" %}
**Note**

For more information on Azure Event Hub audit logs, see [Overview of Azure platform logs](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/platform-logs-overview).
{% endhint %}

| Type of data                                                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Activity logs                                                        | <p>Retrieves events related to the operations on each Azure resource in the subscription from the outside in addition to updates on Service Health events.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong><br><br>These logs are from the management plane.</p></div>                                                                                                                                                                                                                                                                                                      |
| Microsoft Entra ID Activity logs and Microsoft Entra ID Sign-in logs | <p>Contain the history of sign-in activity and audit trail of changes made in Microsoft Entra ID (formerly Azure AD) for a particular tenant.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><br><strong>Note</strong><br><br>Even though you can collect Microsoft Entra ID Activity logs and Microsoft Entra ID Sign-in logs using the Azure Event Hub data collector, we recommend using the Microsoft Office 365 data collector, because it is easier to configure. Do not configure both collectors for the same log types. Doing so creates duplicate data in Cortex XSIAM.<br></p></div> |
| Resource logs, including AKS audit logs                              | <p>Retrieves events related to operations that were performed within an Azure resource.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong><br><br>These logs are from the data plane.</p></div>                                                                                                                                                                                                                                                                                                                                                                               |

{% hint style="info" %}
**Prerequisite**

Ensure that you do the following tasks before you begin configuring data collection from Azure Event Hub.

* Before you set up an Azure Event Hub, calculate the quantity of data that you expect to send to Cortex XSIAM, taking into account potential data spikes and potential increases in data ingestion, because partitions cannot be modified after creation. Use this information to ascertain the optimal number of partitions and Throughput Units (for Azure Basic or Standard) or Processing Units (for Azure Premium). Configure your Event Hub accordingly.
* Create an Azure Event Hub. We recommend using a dedicated Azure Event Hub for this Cortex XSIAM integration. For more information, see [Quickstart: Create an event hub using Azure portal](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create).
* Each partition can support a throughput of up to 1 MB/s.
* Ensure the format for the logs you want collected from the Azure Event Hub is either JSON or raw.
{% endhint %}

Configure the Azure Event Hub collection in Cortex XSIAM:

1. In the Microsoft Azure console, open the **Event Hubs** page, and select the Azure Event Hub that you created for collection in Cortex XSIAM.
2. Record the following parameters from your configured event hub, which you will need when configuring data collection in Cortex XSIAM.

* Your event hub’s consumer group.
  1. Select **Entities** → **Event Hubs**, and select your event hub.
  2. Select **Entities** → **Consumer groups**, and select your event hub.
  3. In the Consumer group table, copy the applicable value listed in the **Name** column for your Cortex XSIAM data collection configuration.
* Your event hub’s connection string for the designated policy.
  1. Select **Settings** → **Shared access policies**.
  2. In the Shared access policies table, select the applicable policy.
  3. Copy the Connection string-primary key.
* Your storage account connection string required for partitions lease management and checkpointing in Cortex XSIAM.
  1. Open the **Storage accounts** page, and either create a new storage account or select an existing one, which will contain the storage account connection string.
  2. Select **Security + networking** → **Access keys**, and click **Show keys**.
  3. Copy the applicable **Connection string**.

3.  Configure diagnostic settings for the relevant log types you want to collect and then direct these diagnostic settings to the designated Azure Event Hub.

    1. Open the Microsoft Azure console.
    2.  Your navigation is dependent on the type of logs you want to configure.

        | Log type                                                             | Navigation path                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
        | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | Activity logs                                                        | Select **Azure services** → **Activity log** → **Export Activity Logs**, and **+Add diagnostic setting**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
        | Microsoft Entra ID Activity logs and Microsoft Entra ID Sign-in logs | <p>1. Select <strong>Azure services</strong> → <strong>Azure Active Directory</strong>.<br>2. Select <strong>Monitoring</strong> → <strong>Diagnostic settings</strong>, and <strong>+Add diagnostic setting</strong>.</p>                                                                                                                                                                                                                                                                                                                                                                                                                         |
        | Resource logs, including AKS audit logs                              | <p>1. Search for <strong>Monitor</strong>, and select <strong>Settings</strong> → <strong>Diagnostic settings</strong>.<br>2. From your list of available resources, select the resource that you want to configure for log collection, and then select <strong>+Add diagnostic setting</strong>.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For every resource that you want to configure, you'll have to repeat this step, or use <a href="https://learn.microsoft.com/en-us/azure/governance/policy/overview">Azure policy</a> for a general configuration.</p></div> |

    c. Set the following parameters:

    * **Diagnostic setting name:** Specify a name for your Diagnostic setting.
    *   **Logs Categories/Metrics:** The options listed are dependent on the type of logs you want to configure. For Activity logs and Microsoft Entra ID logs and Microsoft Entra ID Sign-in logs, the option is called **Logs Categories**, and for Resource logs it's called **Metrics**.

        | Log type                                                             | Log categories/metrics                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
        | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | Activity logs                                                        | <p>Select from the list of applicable Activity log categories, the ones that you want to configure your designated resource to collect. We recommend selecting all of the options.</p><ul><li>Administrative</li><li>Security</li><li>ServiceHealth</li><li>Alert</li><li>Recommendation</li><li>Policy</li><li>Autoscale</li><li>ResourceHealth</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
        | Microsoft Entra ID Activity logs and Microsoft Entra ID Sign-in logs | <p>Select from the list of applicable Microsoft Entra ID Activity and Microsoft Entra ID Sign-in <strong>Logs Categories</strong>, the ones that you want to configure your designated resource to collect. You can select any of the following categories to collect these types of Microsoft Entra ID logs.</p><ul><li><p>Microsoft Entra ID Activity logs:</p><ul><li><strong>AuditLogs</strong></li></ul></li><li><p>Microsoft Entra ID Sign-in logs:</p><ul><li><strong>SignInLogs</strong></li><li><strong>NonInteractiveUserSignInLogs</strong></li><li><strong>ServicePrincipalSignInLogs</strong></li><li><strong>ManagedIdentitySignInLogs</strong></li><li><strong>ADFSSignInLogs</strong></li></ul></li></ul><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>There are additional log categories displayed. We recommend selecting all the available options.</p></div> |
        | Resource logs, including AKS audit logs                              | The list displayed is dependent on the resource that you selected. We recommend selecting all the options available for the resource.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    * **Destination details:** Select **Stream to event hub**, where additional parameters are displayed that you need to configure. Ensure that you set the following parameters using the same settings for the Azure Event Hub that you created for the collection.
      * **Subscription:** Select the applicable **Subscription** for the Azure Event Hub.
      * **Event hub namespace:** Select the applicable **Subscription** for the Azure Event Hub.
      * **(Optional) Event hub name:** Specify the name of your Azure Event Hub.
      * **Event hub policy:** Select the applicable **Event hub policy** for your Azure Event Hub.

    d. Save your settings.
4. Configure the Azure Event Hub collection in Cortex XSIAM.
   1. Navigate to **Settings** → **Data Sources & Integrations**.
   2. On the **Data Sources & Integrations** page, click **+ Add New**, search for **Azure Event Hub**, then hover over it and click **Add**.
   3. Set these parameters:
      * **Name:** Specify a descriptive name for your log collection configuration.
      * **Event Hub Connection String:** Specify your event hub’s connection string for the designated policy.
      * **Storage Account Connection String:** Specify your storage account’s connection string for the designated policy.
      * **Consumer Group:** Specify your event hub’s consumer group.
      *   **Log Format:** Select the log format for the logs collected from the Azure Event Hub as Raw, JSON, CEF, LEEF, Cisco-asa, or Corelight.

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>When you Normalize and enrich audit logs, the log format is automatically configured. As a result, the Log Format option is removed and is no longer available to configure (default).</p></div>
      *   **Vendor and Product:** Specify the Vendor and Product for the type of logs you are ingesting. The Vendor and Product are used to define the name of your Cortex Query Language (XQL) dataset (`<vendor>_<product>_raw`). The Vendor and Product values vary depending on the Log Format selected. To uniquely identify the log source, consider changing the values if the values are configurable.

          <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>When you Normalize and enrich audit logs, the Vendor and Product fields are automatically configured, so these fields are removed as available options (default).</p></div>
      * **Normalize and enrich audit logs:** (Optional) For enhanced cloud protection, you can Normalize and enrich audit logs by selecting the checkbox (default). If selected, Cortex XSIAM normalizes and enriches Azure Event Hub audit logs with other Cortex XSIAM authentication stories across all cloud providers using the same format. You can query this normalized data with XQL Search using the `cloud_audit_logs` dataset.
   4. Click Test to validate access, and then click Enable. When events start to come in, a green check mark appears underneath the Azure Event Hub configuration with the amount of data received.
