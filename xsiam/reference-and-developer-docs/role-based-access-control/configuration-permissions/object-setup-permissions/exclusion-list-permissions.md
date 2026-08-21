---
description: >-
  Control access to manage excluded threat indicators and their exclusion
  settings in Cortex XSIAM.
---

# Exclusion List permissions

Controls access to the indicator exclusion list configuration under **Settings** → **Configurations** → **Object Setup** → **Indicators** → **Exclusion List**. This governs the permanent exclusion of indicators such as IP addresses, domains, URLs, file hashes, and email addresses. It is primarily used for:

* Allowing known-good or trusted infrastructure.
* Suppressing false-positive indicators identified during investigations.
* Filtering noisy vendor feeds that generate high volumes of low-value alerts.

{% hint style="info" %}
### Note

When managing Indicators (located under **Threat Management** → **Threat Intelligence** → **Indicators**), users who lack View/Edit permissions for the Exclusion List will find that exclusion-related features (such as the **Exclusion reason** field and **Do not add to exclusion list** checkbox) are automatically hidden by the system.

Access to the Indicators page itself requires a Threat Intelligence Management (TIM) add-on or a Cortex XSIAM Premium license.
{% endhint %}

| Permission | Description                                                                                                                                      | Roles Example                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | Users cannot view excluded indicators, add new ones, or perform imports/exports.                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| View       | Read-only access to the full table of excluded indicators, including values, types, and comments. Users can search, filter, and export the list. | SOC Tier-1 and 2 Analysts: Should be able to see what is excluded to understand why certain indicators are not flagged, but should not modify the list without approval.                                                                                                                                                                                                                                                                       |
| View/Edit  | Full read/write access. Users can manually add or remove indicators, perform bulk CSV imports/exports, and execute bulk operations.              | <ul><li>SOC Tier 3 Analyst: Can manage exclusions based on advanced threat analysis findings; trusted to add/remove indicators from the exclusion list.</li><li>Threat Hunter: Critical for managing false positive indicators and tuning detection; threat hunters frequently need to exclude known-good indicators.</li><li>Security Engineer: Manages exclusion lists as part of TI pipeline tuning and false positive reduction.</li></ul> |

### Required and recommended permissions

Consider adding the following permissions:

| Permission     | Permission Level  | Reasons                                                                                                                                                                                                                           |
| -------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Threat Intel   | View or View/Edit | <ul><li>View: Required to view indicators that may need exclusion; required to see the Indicators section.</li><li>View/Edit: Strongly recommended to manage indicators alongside exclusions (delete, edit indicators).</li></ul> |
| Cases & Issues | View              | Understand the context of indicators being excluded (which issues they triggered). Strongly recommended.                                                                                                                          |
| Integrations   | View              | View TIM feed integrations that generate the indicators being excluded. Recommended.                                                                                                                                              |
| Audit          | View              | Track who added/removed indicators from the exclusion list. Recommended.                                                                                                                                                          |
