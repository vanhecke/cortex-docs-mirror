---
description: >-
  Use Cortex Cloud Consumption in Cortex XSIAM to monitor cloud security usage
  and consumption.
---

# Cortex Cloud Consumption

The Cloud Consumption Dashboard provides centralized visibility, historical tracking, and granular, account-level auditing for your cloud infrastructure resources. It tracks workload consumption across all connected cloud accounts and providers, breaking the data down by asset type. To simplify multi-cloud deployment tracking, the dashboard normalizes diverse cloud resources into a single, predictable currency called a workload unit.

You can use this dashboard to verify that your cloud workload counts align with your purchased license capacity, to identify which cloud accounts or asset types are driving consumption, and to spot usage trends before they lead to overages.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2F1S875dT0wB0cviHzqHBe%2Fimage.png?alt=media&#x26;token=89c09424-79e0-44d1-8890-9690ff444b89" alt=""><figcaption></figcaption></figure>

### Prerequisites

To view and interact with the dashboard, users and tenants must meet the following conditions:

* **Permissions**: Users must be assigned the Cloud consumption command center permission. This permission is granted by default to Administrator roles and can be manually delegated to custom roles as needed.
* **Licenses**: The dashboard automatically populates if your tenant holds active Cloud Posture Security or Cloud Runtime Security licenses, whether purchased as an individual add-on or a core bundle.
* **Data Collection**: Data must be collected for at least seven days before the Cloud Consumption Dashboard is visible. Historical data is not backfilled in the dashboard.\
  \
  Once the dashboard is visible, the system progressively matures over 90 days, gradually expanding its available date ranges and filtering capabilities as historical data accumulates. During this initial 90-day transition period, the rolling average calculations scale dynamically based on the number of days of data available since the release date. Eventually, data for the past 365 days is available for custom date ranges.

### Workload Unit Conversion

To simplify the complexity of multi-cloud billing, Cortex Cloud normalizes all raw cloud assets into workload units. When counts are aggregated, individual workload unit calculations are mathematically rounded up to ensure precise, predictable billing.

To prevent duplicate charges, workloads discovered by multiple concurrent protection mechanisms (for example, an asset tracked by both a cloud ingestion log and a local host agent) are automatically deduplicated and reported as a single workload unit. Deleted assets and infrastructure managed internally by Palo Alto Networks are excluded from consumption counts.

The following table provides the conversion metrics for mapping protected assets to billable workload units.

<table data-header-hidden><thead><tr><th width="169.5"></th><th width="251.5"></th><th></th></tr></thead><tbody><tr><td>Workload Category</td><td>Asset Type</td><td>Conversion Metric (= 1 Workload Unit)</td></tr><tr><td>Compute</td><td>Scanned VM</td><td>1 Virtual Machine</td></tr><tr><td><br></td><td>Agent Protected Endpoint</td><td>1 Endpoint</td></tr><tr><td>Containers</td><td>Scanned CaaS Instances</td><td>10 Managed Containers</td></tr><tr><td><br></td><td>Registry Scans</td><td>Free Quota: 10 images scanned per deployed workload (VM/CaaS).<br>Beyond Quota: 10 container image scans = 1 Workload.</td></tr><tr><td>Serverless</td><td>Scanned Serverless Functions</td><td>25 Serverless Functions</td></tr><tr><td>Storage &#x26; DB</td><td>Storage Buckets</td><td>10 Cloud Buckets</td></tr><tr><td><br></td><td>PaaS Databases</td><td>2 PaaS Databases</td></tr><tr><td><br></td><td>DBaaS Data Storage</td><td>1 Terabyte (TB) Stored</td></tr><tr><td>Other</td><td>SaaS Users</td><td>10 SaaS Users</td></tr><tr><td><br></td><td>Unmanaged Assets</td><td>4 Unmanaged Assets</td></tr></tbody></table>

### Cloud Consumption dashboard sections

#### Global filters

A unified filter bar at the top of the dashboard allows users to dynamically slice data across all charts and tables simultaneously (excluding the License Summary tiles) by date range, cloud provider, user-defined asset groups (filtered by 'Realm/Account'), and cloud account.

Filtering by date supports data retrieval for the past 365 days.

#### License and entitlement overview

This section acts as an executive summary, bridging purchased licenses with real-time operational usage.

* Global filters do not apply to these tiles.
* The system uses a 90-day rolling average of hourly snapshots to generate these metrics.
* While top-level widgets display rounded billable numbers, moving your cursor over them triggers a tool-tip explaining the exact conversion math (for example, explaining why 85 storage buckets equal 9 workload units).
* If your tenant holds multiple active licenses (such as Cloud Posture Management and Cloud Runtime Security simultaneously), this section automatically generates a separate, dedicated summary row for each license to allow side-by-side tracking.

#### Consumption per asset type

This section outlines the composition of your cloud footprint, identifying which technical asset categories are driving expenditures.

* For views under 7 days, the chart uses an average of hourly snapshots. For custom ranges longer than 7 days, the system displays an average of daily snapshots.
* The chart displays the top 5 highest-consuming cloud providers individually. All other active providers are aggregated and displayed under an Additional category.

#### Consumption over time

This section provides a historical trend line for contract-to-date forecasting, auditing growth trends, and isolating anomalous usage spikes. It charts three distinct boundaries:

* **Purchased**: A static baseline showing the total allocation threshold of your active contract.
* **Used**: The daily average of raw hourly counts collected over a 24-hour cycle, representing your environment's real-time elasticity. The **Cloud Provider** view breaks the **Used** line into individual trend paths for your top 5 cloud environments.
* **Average** (true billable metric): A 90-day rolling average of hourly snapshots calculated once daily. This metric is used to evaluate quota compliance and smooths out short-term operational spikes. For the first 90 days after the dashboard release, the final **Average** values in this chart may differ from the **Cloud runtime security overview** value.

#### Consumption details

This section provides data for troubleshooting and resource mapping.

* If an individual cloud account is deleted or modified, the historical ledger row remains intact, substituting the deleted account name with its unique Cloud Account ID.
* You can download filtered data as a standard TSV/CSV file.
* Workload-centric data- unlike standard asset inventory screens, this table displays numbers natively in workload units, not raw asset counts, aligning directly with your billing logic.
* \* Advanced search & customization- features a backend-supported search bar to find accounts instantly by name or provider, and an interactive Column Picker to show or hide specific security categories (like CSPM or Agentless) active on each account.
