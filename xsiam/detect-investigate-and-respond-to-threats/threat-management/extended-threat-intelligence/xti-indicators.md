---
description: >-
  Investigate, manage, and enrich threat indicators, including domains, IP
  addresses, URLs, and file hashes.
---

# XTI Indicators

XTI Indicators help you identify and investigate suspicious or malicious activity.

## Indicator concepts

XTI indicators are observables, structured representations of stateful properties or measurable events within a cyber environment, such as IP addresses and file hashes. Unlike the threat objects in the Threat Intel Library, indicators are high-volume, and, in some cases, frequently changing items that are used to identify malicious or suspicious activity, or other activity associated with security issues. XTI indicators include Indicators of Compromise (IOCs) and other non-malicious indicators.

### Indicator types

XTI currently supports the following indicator types:

* Domains
* File hashes (SHA-256)
* IP addresses
* URLs

{% hint style="info" %}
Only IPv4 addresses are currently supported. IPv6 addresses are not supported.
{% endhint %}

### Common indicator data model

XTI Indicators share a set of common fields, such as Verdict, Creation Method, Tags, First Seen, and Last Seen.

Additionally, each indicator type includes unique fields; for example, File Type and File Size are specific to file hashes.

### Indicator verdict

XTI assigns an indicator verdict according to the verdict returned by the source with the highest reliability.

Indicators are assigned the following verdicts:

* Unknown
* Benign
* Suspicious
* Malicious

The verdict can be modified by a user.

### Indicator input sources

There are three primary sources for adding indicators to the XTI Indicators dataset:

| **Source**                         | **Description**                                                                                                                                                                                                                                      |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unit 42 first-party data ingestion | <p>First-party indicators are powered by high-fidelity Unit 42 data and are sourced from the entire Palo Alto Networks product suite.</p><p>Unit 42 indicators are added through periodic feed ingestion every 24 hours.</p>                         |
| Automated extraction               | <p>Potential indicators are automatically extracted from Issue objects, enriched with Unit 42 intelligence, and added to the XTI Indicators dataset.</p><p>Indicators extracted from issues are added in near real-time as issues are processed.</p> |
| User creation                      | Users can manually create or import indicators, adding them to the XTI Indicators dataset.                                                                                                                                                           |

When reviewing the list of indicators, the **Creation Method** field indicates the original source of a specific indicator. The **Last Modification Method** field indicated the source that last updated the indicator.

## Indicator lifecycle

Indicator lifecycle management defines how indicators evolve, how conflicting data is handled, and how metadata remains accurate over time.

It consists of several core automated and manual processes:

| **Step**                                | **Details**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Automatic ingestion and enrichment      | Indicators are continuously managed through periodic feed ingestion from Unit 42. To keep metadata fresh, the system performs periodic background enrichments.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Normalization and deduplication         | Because indicators can come from multiple sources (such as an extraction from an issue or ingestion from a Unit 42 feed), the system normalizes the data and deduplicates it into a single "golden record" based on the indicator's value and type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| User overrides (verdict and expiration) | <p>A user can manually update the following indicator fields:</p><ul><li>Verdict</li><li>Expiration</li><li>Tags</li></ul><p>If a user manually updates a field, that field is "detached" from future automatic updates to preserve the user's input. The system visually flags this field as "Out of Sync," and users can select "Revert to Automatic Update" if they want to unlock it and resync with the latest upstream threat intelligence.</p><p>If a user manually changed the verdict for an indicator, when a new verdict update is available for that indicator from the upstream threat intel source, a user can review and apply the update.</p>                                                                                                                                                                                                                                                          |
| Creation of indicators by user          | Users can manually add indicators, entering the specific domain, file hash, IP address or URL associated with the indicator and optionally specifying the verdict.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Indicator expiration                    | <p>Indicators are automatically marked as “Expired" based on fixed time windows since the last sighting, the last update, or the last extraction. By default, IPs expire in 7 days, domains in 14 days, URLs in 30 days, and file hashes never expire. A user can also manually expire indicators (individually or in bulk). Expired indicators are removed from active threat matching but are kept in the dataset up to a certain period of time to provide historical context for investigations.</p><p>An expired indicator is automatically reactivated—or "unexpired"— in the following scenarios:</p><ul><li>If it is observed again within a threat feed or via enrichment.</li><li>If its verdict is manually updated.</li><li>If its associated tags are edited.</li></ul><p>When any of these conditions are met, the platform immediately resets the indicator's expiration status to <em>Active</em>.</p> |

### Edit an indicator verdict

You can edit the verdict of an indicator.

1. Go to **Threat Management → Threat Intelligence → Indicators**.
2. Select a specific indicator to go to its Overview.
3. Position the cursor over the **Verdict** field until an edit tooltip appears next to it.
4. Select the edit tooltip next to the Verdict.
5. Provide the following information:
   1. **Verdict**: Select a new verdict.
   2. **Verdict Change Reason**: Select the reason for the verdict change (**False Positive** or **Other**).
   3. **Additional Comments** (Optional): You can provide additional information.
6. Select **Apply**.

After the verdict update is complete, position the cursor over the **Verdict** field and you should see “Verdict set by {user name}”.

### Apply a verdict update

If a user manually changed the verdict for an indicator, when a new verdict update is available for that indicator from the upstream threat intel source, a user can review and apply the update.

### Expire indicators

You can expire a single indicator or “bulk-expire” multiple selected indicators.

1. Go to **Threat Management → Threat Intelligence → Indicators**.
2. Select one or more indicators.
3. Select the **Expire** button, or right-click an indicator and select **Expire**.

After an indicator has expired, its Expiration Status changes from “Active” to “Expired”.

### Tag indicators

You can apply tags to indicators to provide context for filters, XQL queries, and playbooks.

1. Go to **Threat Management → Threat Intelligence → Indicators**.
2. Select a specific indicator to go to its Overview.
3. In the **Tags** section, select the edit tooltip to modify tags.
4. Add the tags and select **Apply**.

### Add an indicator

1. Go to **Threat Management → Threat Intelligence → Indicators**.
2. Select **+Add New Indicator**.
3. **Single indicator** tab is pre-selected. Provide the following information:
   1. **Type**: Select one of the supported indicator types (Domain, File hash, IP address, URL).
   2. **Value:** Enter the specific domain, file hash, IP address or URL associated with the indicator. If an indicator with that value already exists, the UI returns an error message.
   3. **Verdict** (Optional): Select one of the following: Unknown, Benign, Suspicious, Malicious
4. Select **Add**.

## Investigate Indicators

The **Indicators** page lists domains, IP addresses, URLs, and file hashes.

You can access it from **Threat Management → Threat Intelligence → Indicators**.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FvOj9WpsXupigijGd3voF%2Funknown.png?alt=media&#x26;token=9fbebbb6-869d-4d7a-8b3c-56a4744cbeba" alt="This screenshot from Cortex UI shows the XTI Indicators page listing indicators." height="415" width="624"><figcaption></figcaption></figure>

You can use this page to view data and discover relationships between specific indicators and the broader threat landscape. The main tab contains all indicators and you can also view dedicated tabs for **Domain**, **File Hash**, **IP**, and **URL** indicator types.

The widgets at the top of the page provide visualizations that help you understand the breakdown of the indicators by type, verdict, and association with threat objects.

You can search and filter by fields such as value, type, threat actors, malware families, verdict, and tags.

When you select an indicator, a side pane opens, providing highlights designed for rapid tactical assessment and information about related threat actors and malware families.

* **Overview**: Shows highlights such as description, summary, and tags.
* **Detections**: Lists cases and issues associated with the specific indicator, including cases based on direct IOC observation and cases based on Behavioral Threat Analysis (BTA). Select a **Cases** or **Issues** grouping to view cases or issues in a tabular view.
* **Associations**: Lists related Threat Actors and Malware Families.
* **Reports**: Shows reports related to the indicator.

\
<br>
