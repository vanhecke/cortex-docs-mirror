---
description: >-
  Save your ingested, parsed data in an external location by exporting your
  event logs to a temporary GCP storage bucket.
---

# Manage Event Forwarding

{% hint style="warning" %}
Currently, Event Forwarding via Google Pub/Sub is not supported for third-party destinations that require subscription discovery permissions, such as Splunk, Cribl, or Security Onion. These solutions typically require additional Google Cloud permissions, such as `pubsub.subscriptions.get`, that are not provided by the default Cortex XSIAM service account role. Before configuring event forwarding, verify if your destination requires subscription discovery or specific metadata parameters that exceed the standard **Pub/Sub Subscriber** role.
{% endhint %}

{% hint style="info" %}
### Prerequisite

Event Forwarding requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Dataset Management.
{% endhint %}

You can save your ingested, parsed data in an external location by exporting your event logs to a temporary storage bucket on Google Cloud Platform (GCP).

{% hint style="info" %}
After exporting logs, you can download them from GCP for up to 14 days. The Pub/Sub subscription messages are available for 7 days.
{% endhint %}

Event forwarding has the following purposes:

* Compliance: You may have specific compliance requirements to retain logs in a separate, secure environment for long-term storage or auditing purposes.
* Long-term archive: The core function is to export the event logs that the tenant has ingested and parsed to a storage location outside of the XSIAM tenant. This provides you with a copy of the normalized and processed data.
* External analytics: Download the exported event logs for use in other security tools, data analysis platforms, or for offline forensic investigation.

You can forward the following events to GCP:

*   Endpoints Event Forwarding

    Forwards raw, high-fidelity security telemetry collected by EDR, including data from endpoints through the XDR Agent and cloud workloads (VMs, containers, or third-party EDRs). The exported logs are raw data, without any stories, and export a subset of the endpoint data without filtering or configuration options. For more information about the type of information forwarded, see [Endpoints Event Forwarding - included/excluded fields by event type](manage-event-forwarding/endpoints-event-forwarding-included-excluded-fields-by-event-type).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Requires the Endpoints Event Forwarding add-on.</p></div>
*   GB Event Forwarding

    Covers all other security data measured by daily ingestion volume (in Gigabytes). This includes non-endpoint logs such as firewall traffic, cloud audit logs, network flow logs, identity data, and general Syslogs from servers and devices. The exported logs are raw data, without any stories, and export all the data without filtering or configuration options.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Requires the GB Event Forwarding add-on</p></div>

Use the **Event Forwarding** page to activate Event Forwarding, to retrieve the path and credentials of your external storage destination on GCP. Once this page is activated, Cortex XSIAM automatically creates the GCP bucket.

{% hint style="info" %}
### Important

Since data is aggregated and compressed, it may take up to two hours until the data is available in the forwarding bucket.
{% endhint %}

### Upload to a temporary GCP storage bucket

Before you begin, ensure that you have the view/edit permission for Data Management. Instance Administrators have this permission by default.

1. Under **Settings** → **Configurations** → **Data Management** → **Event Forwarding**, activate one or more of the following:
   * **Enable GB Event Forwarding**
   * **Enable Endpoints Event Forwarding**
2.  **Save** your selection.

    The **Destination** section displays the details of the GCP bucket created by Cortex XSIAM, where your data is stored for 14 days. The data is compressed and saved as a line-delimited JSON gzip file.
3. Access GCP Cloud Storage using a Service Account.
   1. **Copy** the storage path displayed.
   2.  **Generate and download** the Service Account JSON WEB TOKEN, which contains the access key.

       Save it in a secure location. If you need to regenerate the access token, **Replace and download** a new token. This action invalidates the previous token.

       The token provides access to all your data stored in this bucket. It must be saved in a safe place.

       Use the storage path and access key to manually retrieve your files or use an API for automated retrieval.
   3. Using the storage path and access key, retrieve your files manually or using an API.
      * [Authenticating as a service account](https://cloud.google.com/docs/authentication/production)
      * [Copying files and objects from GCP](https://cloud.google.com/storage/docs/gsutil/commands/cp)
4. (Optional) Use the Pub/Sub subscription to ensure reliable data retrieval without any loss.
   1. **Copy** the Pub/Sub subscription provided.
   2.  Configure your application or system to receive messages from the Pub/Sub subscription.

       Whenever a new file is added to the GCS bucket, a message is sent to the Pub/Sub subscription. The object path of the file in the bucket has the prefix `internal/`.
   3. Process the received message to initiate the download of the corresponding file.
