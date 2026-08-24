---
description: Manage Cortex XSIAM compute units for API, Apps, and Cold Storage XQL queries.
---

# Manage compute units

Cortex XSIAM uses compute units (CU) for these types of queries:

* API Queries: When running Cortex Query Language (XQL) queries on your data sources using APIs, each XQL query API consumes CU based on the timeframe, complexity, and number of API response results.
* Apps: The Notebooks instance consumes 1000 CU each day, and BigQuery queries consume CU based on the timeframe, complexity, and number of results. Apps are charged daily at 00:00 UTC.
*   Cold Storage Queries: Cold Storage is a data retention offering for cheaper storage, usually for long-term compliance needs, with limited search options. You can perform queries on Cold Storage data using the following dataset formats:

    * For typical cold storage queries: `cold_dataset = <dataset name>`
    *   For historical data imported into cold storage queries: `cold_dataset = archive_<dataset name>`.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>For more information, see <a href="archived-data/import-historical-data-into-cold-storage">Import historical data into cold storage</a>.</p></div>

    These cold storage queries consume CU according to the following calculations:

    * Amount of data queried. 1CU for querying 35GB of data.
    * Timeframe, complexity, and the number of Cold Storage response results of each XQL Cold Storage query.

    When you query Cold Storage data, the rewarmed data is saved in a temporary hot storage cache that is available for subsequent queries on the same time range at no additional cost. The rewarmed data is available in the cache for 24 hours, and on each re-query, the cached data is extended for 24 hours, for up to 7 days.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The CU consumption of cold storage queries is based on the number of days in the query time frame. For example, when querying 1 hour of a specific day, the CU of querying this entire day is consumed. When querying 1 hour that extends past 2 days, such as from 23:50 to 00:50 of the following day, the CU of querying these two days is consumed.</p></div>

{% hint style="info" %}
### Important

Agentic and LLM information is shown only for informational purposes and does not currently consume compute units.
{% endhint %}
