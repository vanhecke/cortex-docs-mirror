# Search permissions

Configure access to threat hunting, querying, and forensic data collection tools, including the Query Library, Query Center, Forensics, Host Insights, and Graph Search.

{% hint style="warning" %}
### Caution

* Dataset Access (SBAC) Requirement: Even with full Query Center access, queries will return empty results or errors if the user lacks the specific dataset permissions (configured per dataset).
* Query Library/Center: If you want users to execute and schedule queries from the Query Library, they must have View/Edit permission in the Query Center. To save queries directly from the Query Center to the Library, they need View/Edit in the Query Library.
{% endhint %}
