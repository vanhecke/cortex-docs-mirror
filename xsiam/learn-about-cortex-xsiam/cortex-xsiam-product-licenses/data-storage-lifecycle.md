---
description: >-
  Understand the Cortex XSIAM data storage lifecycle, including hot and cold
  storage, retention extensions, and Event Forwarding exports.
---

# Data storage lifecycle

Cortex XSIAM data storage is managed in the Cortex XSIAM Data Layer. You receive data storage based on the amount associated with your licenses, determined by factors such as daily ingestion needs and the number of users. All licenses provide default retention periods, which can be extended for hot and cold storage.

To determine your requirements, you must understand the differences between the available storage options. The following image shows examples of these differences:

![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4bf55a15315a2d858ff0eb96f2847a00f9500e72%2F27dd6b30ab1279048b24187ba6a8b4e9dd52b50a4f53d20905cd0b9b8d4c2c92.png?alt=media)

<details>

<summary>Data Ingestion Pipeline</summary>

Data enters via a data stream called the Data Ingestion Pipeline, where manipulation, such as normalization, enrichment, and analytics, occurs. Once ready, it is transferred to the following locations based on your licenses:

</details>

<details>

<summary>Hot storage</summary>

With a regular license, data is automatically sent to hot storage for the default retention period (typically one month).

* **Extensions**: You can add retention in monthly increments via Period-Based Retention (all data) or Additional Hot Storage (specific datasets).
* **Retroactive application**: If you purchase additional hot storage, the new retention time can be applied retroactively to any data still available in your hot datasets that hasn't been rolled out yet.
* **Image example**: In the image above, the regular Cortex XSIAM license and additional storage licenses ensure that all the data is accessible from hot storage for two months. After this, data begins purging except for Dataset 2 (accessible for one additional month) and Dataset 3 (accessible for two additional months) before being gradually purged.

</details>

<details>

<summary>Cold storage</summary>

A regular license provides no default cold storage.

*   **Independence**: There is no connection between hot and cold storage; you cannot move missing data from hot to cold storage later. Data must be sent to cold storage from the pipeline starting from the purchase date.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>If you want your cold storage data to align with the hot storage data, you must ensure you purchase your cold storage license at the same time as your regular Cortex XSIAM license.</p></div>
* **Accessibility**: Cold storage data is collected upon ingestion but is only accessible after the hot storage retention period has expired. The cold storage retention period only begins once the hot storage period ends.
* **Retroactive application**: If you purchase additional cold storage, the extra retention time may be applied retroactively to any data still residing in your cold datasets that hasn't been rolled out yet, provided the existing data is covered under the renewal/purchase.
*   **Requirements**: Requires a minimum of six months of retention and Compute Units (CU) to run cold storage queries. For more information on CU, see [Manage compute units](../../configure-cortex-xsiam/data-management/manage-compute-units).

    For information on the CU add-on license, see [Understand the Cortex XSIAM license plan]().
* **Image example**: Cold storage is aligned with hot storage. The pipeline sends data to both for the first two months, but it is not accessible in cold storage during the hot storage retention period. After two months, the data becomes accessible in cold storage for six months (except for Datasets 2 and 3, which are still in their extended hot storage periods). Once those datasets finish their hot retention, they also become accessible in cold storage for six months before purging.

</details>

<details>

<summary>Export</summary>

A regular license does not provide default export capabilities.

* **Event Forwarding**: Only after purchasing this add-on is data sent to an intermediate storage location from the pipeline.
* **Retention**: This data is accessible for seven days before being gradually purged.
*   **Image example**: Export data is aligned with hot and cold storage. The pipeline sends data to intermediate storage for Event Forwarding, which is accessible for seven days before purging.

    For more information on Event Forwarding, see [Manage Event Forwarding](../../configure-cortex-xsiam/data-management/manage-event-forwarding).

</details>

<details>

<summary>Recommendations</summary>

To optimize your data strategy and prevent data loss, consider the following best practices:

* **Synchronize license purchases**: For your cold storage data to align perfectly with your hot storage data, you must purchase your cold storage license at the same time as your regular Cortex XSIAM license. This ensures the Data Ingestion Pipeline begins feeding both streams simultaneously from day one.
* **Manage retention proactively**: To ensure no data is lost and that extensions can be retroactively applied to your hot and cold datasets, always make changes to your data retention licenses while the current license is still active. If a license expires or the data retention period passes, the data is purged and cannot be recovered or extended retroactively.

</details>

{% hint style="info" %}
You can view details about your Cortex XSIAM licenses by selecting **Settings** → **Cortex XSIAM License**.
{% endhint %}
