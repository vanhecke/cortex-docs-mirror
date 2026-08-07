---
description: >-
  Configure how Cortex XSIAM extracts indicators from tasks, scripts, and
  integrations.
---

# Indicator extraction

Indicator extraction identifies indicators from different text sources in the system (such as War Room entries and email content), extracts them (usually based on regex), and creates indicators in Cortex XSIAM . After extraction, the indicator can be enriched.

Indicator enrichment takes the extracted indicator and provides detailed information about the indicator, based on enrichment feeds such as VirusTotal and IPinfo.

{% hint style="info" %}
### Note

By default, system-wide automatic indicator extraction and enrichment is disabled. However, if you migrated from Cortex XSIAM 2.x to Cortex XSIAM 3.x, system-wide automatic indicator extraction and enrichment is enabled.

If you have a Threat Intel Management (TIM) Add-on, you can enable or disable automatic indicator extraction system-wide. Go to **Settings** → **Configuration** → **General** → **Server Settings**. In the **Indicators** section, enable **Enable automatic indicator extraction and enrichment from issues**.
{% endhint %}

To extract indicators from incoming feeds without enrichment or to prevent enrichment for existing indicators, see [Exclude indicators from enrichment](exclude-indicators-from-enrichment).

In Cortex XSIAM, the indicator extraction feature extracts indicators from War Room entries and enriches them using commands and scripts defined for the indicator type.

You can extract indicators in the following scenarios:

* When fetching issues
* In a playbook task
* Using the command line

{% hint style="info" %}
### Note

Reputation commands, such as **`!ip`** and **`!domain`**, can only be used after you configure and enable a reputation integration instance, such as VirusTotal and Whois.
{% endhint %}

**Indicator extraction modes**

You set the indicator extraction mode:

* In a [playbook task](indicator-extraction/set-the-indicator-extraction-mode-for-a-playbook-task).
* Running a [command](../indicator-investigation/extract-and-enrich-an-indicator) during an investigation.

Indicator extraction supports the following modes:

* **None**: Indicators are not extracted automatically. Use this option when you do not want to further evaluate the indicators.
* **Inline**: Indicators are extracted within the context that indicator extraction runs (synchronously). The findings are added to the context data. For example, if indicator extraction mode for a task in a playbook is inline, the extraction and enrichment must complete before the next task begins. This option provides the most robust information available per indicator.
  *   <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The inline configuration may delay playbook execution.</p></div>

      <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>While indicator creation is asynchronous, indicator extraction and enrichment are run synchronously. Data is placed into the issue context and is available via the context for subsequent tasks.</p><p>All indicators are automatically extracted and enriched before a playbook is run. For an on-field change, extraction occurs before the next playbook tasks run.</p></div>
*   **Out of band**: Indicators are extracted in parallel (asynchronously) to other actions. The extracted data will be available within the issue, however, it is not available for immediate use in task inputs or outputs since the information is not available in real-time.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>When using out of band, the extracted indicators do not appear in the context. If you want the extracted indicators to appear select inline.</p></div>
* If system-wide indicator extraction and enrichment is enabled, indicators are extracted according to the following system defaults:
  * Issue creation - inline
  * Tasks - none, can be overridden on a per task basis
  * CLI - out of band, but can be overridden on a per-command basis

**Troubleshoot indicator extraction**

If indicators are not extracted, check whether the indicator mode is set to none, and verify the indicator is not in the Exclusion List, as is or as part of a regular expression (regex).
