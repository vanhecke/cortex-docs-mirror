---
description: >-
  Configure access to threat hunting, query, and forensic investigation tools in
  Cortex XSIAM.
---

# Search permissions

Configure access to threat hunting, querying, and forensic data collection tools, including the Query Library, Query Center, Forensics, Host Insights, and Graph Search.

* [query-library-permissions](search-permissions/query-library-permissions "mention")
* [query-center-permissions](search-permissions/query-center-permissions "mention")
* [forensics-permissions](search-permissions/forensics-permissions "mention")
* [host-insights-permissions](search-permissions/host-insights-permissions "mention")
* [graph-search-permissions](search-permissions/graph-search-permissions "mention")

{% hint style="warning" %}
- Dataset Access (SBAC) Requirement: Even with full Query Center access, queries will return empty results or errors if the user lacks the specific dataset permissions (configured per dataset).
- Query Library/Center: If you want users to execute and schedule queries from the Query Library, they must have View/Edit permission in the Query Center. To save queries directly from the Query Center to the Library, they need View/Edit in the Query Library.
{% endhint %}
