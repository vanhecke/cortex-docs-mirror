---
description: Use enhancement scripts to add threat intelligence context to indicators.
---

# Enhancement scripts

Enhancement scripts enable you to gather additional data about the highlighted entry in the War Room. They can enrich indicators, search a SIEM for a specific indicator, write indicator details to context, and return entries to the War Room.

Enhancement scripts are run manually from the **Indicator Quick View** window or the CLI after indicators are extracted to allow you to collect additional information about an indicator. If you have an issue that contains an IP indicator and you want to run one or more enhancement scripts, go to **Indicator Quick View** → **Actions** and under **Run Scripts**, select the desired script.

{% hint style="info" %}
### Note

Enhancement scripts are different from reputation commands. A reputation command runs every integration that has that command within it, to enrich the indicator. The reputation command **`ip`** , for example, runs every IP integration command in your enabled integrations, to collect data from multiple sources. An enhancement script is manually run after the initial extraction and enrichment for the indicator type is complete.
{% endhint %}

<details>

<summary>Enhancement script input</summary>

The enhancement script requires the indicator value as the input argument.

| Argument                   | Description                                                                                                                                                                                                                                         |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The value of the indicator | For example **`ip`**, **`email`**, **`url`**.The argument name should match the indicator type in lower case. For example, the **`IPReputation`** script requires the **`ip`** input. For an **`EmailReputation`** script the input is **`email`**. |

In the following example, the **`DomainReputation`** script uses **`domain`** as the input.

![domain-rep-8-input.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6c0b4b2f00b07dd99951ed7d780f3f750429d733%2F1bf296eaaf935d9e49a0b59fb191b011bb413824da640d8d1b989a3a67cfebc7.png?alt=media)

</details>

<details>

<summary>Enhancement script outputs</summary>

The enhancement script output depends on its input because the script is run manually. If you want the output to be added to indicator enrichment or the Threat Intelligence screen, it should follow the DBotScore convention in the content output as described in [https://xsoar.pan.dev/docs/integrations/dbot](https://xsoar.pan.dev/docs/integrations/dbot).

```programlisting
output =
   {
       'Type': entryTypes['note'],
       'ContentsFormat': formats['json'],
       'Contents': ‘this is the enrichment data’,
       'EntryContext': {
           'Email': ‘xsoar@test.com’, 
           ‘DBotScore’: {}},
   }

return_results(output)
```

</details>

<details>

<summary>Add an enhancement script to an indicator type</summary>

1. Go to Settings → Configurations → Object Setup → Indicators → **Types**
2. Select the indicator type and click **Edit**.
3.  Select one or more desired enhancement scripts.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Enhancement scripts must have the <strong><code>enhancement</code></strong> tag applied to appear in the list.</p></div>

</details>

<details>

<summary>Run an enhancement script in the CLI</summary>

You can run out-of-the-box or custom enhancement scripts in the CLI to enrich specific indicator values.

The following are examples of the syntax for running the out-of-the-box `IPReputation` and `URLReputation` enhancement scripts in the CLI.

* **`!IPReputation ip=8.8.8.8`**
* **`!URLReputation url=cardcom.com`**

</details>
