---
description: Use Federated Search to query external data sources in Cortex XSIAM.
---

# Federated Search

Federated Search is a query mechanism designed to provide unified access to distributed data sources without requiring pre-ingestion or centralization. This capability enables you to query data in place, significantly reducing the complexity and operational costs associated with the ingestion process and long-term data retention.

{% hint style="info" %}
Federated Search is not enabled by default. To enable it in your tenant, contact your Customer Support Team.
{% endhint %}

Modern enterprises store massive volumes of data across multiple cloud providers and hybrid environments. Centralized data ingestion and warehousing may be insufficient or expensive for cold or regulatory-mandated data. Federated Search allows you to:

* De-couple data management from data analytics for cost optimization.
* Maintain economic solutions for long-term data storage.
* Perform on-demand incident response or compliance audits against existing long-term storage solutions without the overhead of ingestion.

The main use cases for Federated Search include:

* Incident Investigation: Querying events that occurred a long time ago, where the data might not have been ingested into Cortex XSIAM.
* Compliance audits: Accessing historical data needed for audits without the need for extensive ingestion.
* Long-Term data storage: Providing an integrated solution for retaining data for many years.
* Data linking: Joining external datasets with ingested datasets for comprehensive and unified data analysis.

You can keep non-critical, high-volume data types in their native storage locations while preserving the ability to query this data using Cortex Query Language (XQL). This ensures that visibility is gained into a broader spectrum of data while maintaining the core value proposition of deep analytics on ingested data.

{% hint style="info" %}
Federated search queries consume compute units, which are calculated according to timeframe, complexity, and any cross-cloud egress costs that may apply.
{% endhint %}

### Supported configurations

Federated Search supports the following configurations.

| PROPERTY                    | CONFIGURATION                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Storage solutions           | <p>Amazon Web Services (AWS) S3<br>Google Cloud Storage (GCS)<br>Azure Blob Storage</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Formats                     | <p>CSV<br>Parquet<br>JSONL<br><br><strong>NOTE:</strong><br>For optimal results, we recommend the Parquet format. Federated Search supports certain use cases of gzip compressed files. For additional information, please contact your support agent.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Partitioning/File Structure | Your data must be partitioned and must follow the Hive partitioning format, which uses key-value pairs. Partitions must be named in the yyyy-mm-dd format (for example, ds=2023-07-07).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Supported Regions           | <p><strong>AWS:</strong> us-east-1, us-west-2, ap-northeast-2, ap-southeast-2, eu-west-1, eu-central-1<br><br><strong>GCS:</strong> africa-south1, asia-east1, asia-east2, asia-northeast1, asia-northeast2, asia-northeast3, asia-south1, asia-south2, asia-southeast1, asia-southeast2, australia-southeast1, australia-southeast2, europe-central2, europe-north1, europe-north2, europe-southwest1, europe-west1, europe-west10, europe-west12, europe-west2, europe-west3, europe-west4, europe-west5, europe-west8, europe-west9, me-central1, me-central2, me-west1, northamerica-northeast1, northamerica-northeast2, northamerica-south1, southamerica-east1, southamerica-west1, us-central1, us-east1, us-east4, us-east5, us-south1, us-west1, us-west2, us-west3, us-west4<br><br><strong>Azure Blob Storage:</strong> eastus2<br><br><strong>NOTE:</strong><br>The list of supported regions may change in the future.</p> |

### Limitations

The following limitations apply to Federated Search:

| LIMITATION | DESCRIPTION                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Regions    | <p>If your tenant is on a specific region server (and not on a multi-region server), the bucket must be in the same region as your tenant.<br><br>If your tenant is on a multi-region server, you can only configure regions that are in the multi-region of your tenant. The bucket must be in the same multi-region as your Cortex tenant. For example, if your Cortex XSIAM tenant is located in the US multi-region, you can configure an external dataset only from regions in the US multi-region.</p> |
| Queries    | <p>The following functions are not available in Federated Search and remain exclusive to fully ingested data:<br><br></p><ul><li>Complex, cross-source analytical functions, for example correlations, widgets, dashboards, playbooks, and APIs.</li><li>search, target and view XQL stages.</li></ul>                                                                                                                                                                                                       |
