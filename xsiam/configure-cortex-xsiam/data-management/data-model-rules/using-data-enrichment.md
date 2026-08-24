---
description: Use data enrichment with Cortex XSIAM Data Model Rules.
---

# Using data enrichment

{% hint style="warning" %}
### Prerequisite

Data Model Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Parsing Rules, and Event Forwarding.
{% endhint %}

Cortex XSIAM automatically enriches your Cortex Data Model (XDM) data with additional information and context. Some examples of the types of data that are enriched include:

{% hint style="info" %}
### Note

For a complete list of auto-enriched fields, see the [XSIAM Data Model Schema](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/).
{% endhint %}

* IP addresses are enriched with geolocation information.
* User data is normalized.
* If DSS exists, it is also enriched.

These enrichments are important for cyber analytics, rule detection, and investigations. Since these fields are enriched automatically by default, they do not have to be mapped manually in Data Model Rules. Note that enrichment is not performed when the input fields needed for enrichment are not available.

Enriched data is calculated by the system upon ingestion, and is saved for future queries. Keep in mind that some data may change over time, such as IP addresses that may change geolocation. Therefore, checking the same IP address in external systems at a later time might return a different geolocation result.

<details>

<summary>Overriding Data Enrichment</summary>

We do not recommend overriding enriched fields. However, if enriched fields are not desired, they can be overridden by mapping data to fields that are usually enriched.

```programlisting
[MODEL: dataset=okta_sso_raw]
| alter xdm.source.ip = actor->ip_address,
      xdm.source.location.country = actor->country,
      xdm.source.location.city = actor->geo.city;
```

When overriding enriched fields, ensure the following:

* The overridden data should be normalized.
* All relevant enriched fields should be overridden (for example, all location fields), and empty values should be filled with “unknown” (or with NULL, if calculated enrichments are desired). These actions will prevent data mismatch and conflicts.

{% hint style="info" %}
### Important

When manually mapping ASN fields that are enriched, such as `xdm.source.asn.as_number`, with other ISP and domain fields that are not enriched, such as `xdm.source.asn.isp` and `xdm.source.asn.domain`, it's possible to receive incorrect XDM query results due to the misalignment between the overridden enrichement and system enrichment fields.
{% endhint %}

</details>

<details>

<summary>Limitations</summary>

* Geolocation limitations
  * Some values will be NULL if the log country doesn't match the country detected by an external geolocation tool.
  * There might be discrepancies when some data come from the log and other data from the enrichment. For example, log country data versus enrichment longitude data.
* Data enrichment is not performed for EDR events.
* This feature is not supported in cold storage.

</details>

<details>

<summary>Backward compatibility</summary>

Data ingested by versions prior to Cortex XSIAM version 1.3 will not be enriched, because enrichment is calculated at the time of ingestion.

By default, enrichment is performed for NULL values only (non-NULL values are not overridden). Therefore, some existing mapping rules may need to be updated, in order to prevent mapping data to the enriched fields. Contact Customer Support for assistance with converting custom modeling rules and saved queries.

</details>
