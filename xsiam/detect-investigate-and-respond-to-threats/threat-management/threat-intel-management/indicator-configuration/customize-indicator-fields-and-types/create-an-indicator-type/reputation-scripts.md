---
description: Use reputation scripts to calculate or update an indicator's reputation.
---

# Reputation scripts

Reputation scripts are used to assess and assign reputation scores to indicators. These scripts integrate external threat intelligence or internal data sources to evaluate the reputation of indicators (such as IP addresses, URLs, or file hashes). Reputation scripts enable you to implement custom logic and algorithms for determining the reputation of indicators.

Reputation scripts return the verdict of an indicator as a number. The number overrides the verdict returned from the reputation command and any default settings for the indicator that relates to the verdict, but does not override a manually set verdict.

The system automatically executes the reputation script in the following cases:

* During enrichment: When enrichment is triggered (via indicator extraction, the **`enrichIndicators`** command, or the **Enrich** button), the system runs the reputation command and then the reputation script for the specific indicator type.
* If a verdict changes not via the enrichment process: When explicitly running a reputation command such as **`!file`**, if the result changes the indicator's verdict the reputation script runs to finalize the decision. This happens even if you use the **`using`** argument to target a specific integration.

The reliability of the score from a reputation script is by default `A++ - Reputation script`.

Out-of-the-box reputation scripts

You can create a new reputation script, or you can use an out-of-the-box reputation script in the **Scripts** page, for example:

* `CertificateReputation`
* `cveReputation`
* `MaliciousRatioReputation`
* `SSDeepReputation`

<details>

<summary>Reputation Script input</summary>

The reputation requires a single input argument named **`input`** that accepts an indicator value.

| Argument | Description          |
| -------- | -------------------- |
| `input`  | The indicator value. |

![reputation-script-8-set.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-17ced79f8bfab47783fd8ec3e21611a45a595e22%2F56a7e2f9471a912ffc6450142b176b75348f8e4f767dd1e7e4b4c8b22935be28.png?alt=media)

</details>

<details>

<summary>Reputation Script outputs</summary>

Either a number or a [dbotScore](https://xsoar.pan.dev/docs/integrations/dbot). It can either be a raw number which is the score, or a full entry with DBotScore.

```programlisting
from CommonServerPython import *


def main():
    url_list = argToList(demisto.args().get('input'))
    entry_list = []

    for url in url_list:
        entry_list.append({
            'Type': entryTypes['note'],
            'ContentsFormat': formats['json'],
            'Contents': 2,
            'EntryContext': {
                'DBotScore': {
                    'Indicator': url,
                    'Type': 'Onion URL',
                    'Score': 2,  # suspicious
                    'Vendor': 'DBot'
                }
            }
        })

    demisto.results(entry_list)


if __name__ in ('__main__', 'builtin', 'builtins'):
    main()
```

</details>

<details>

<summary>Values for Common.DbotScore</summary>

| Constant                    | Value          |
| --------------------------- | -------------- |
| Common.DbotScore.NONE       | NONE = 0       |
| Common.DbotScore.GOOD       | GOOD = 1       |
| Common.DbotScore.SUSPICIOUS | SUSPICIOUS = 2 |
| Common.DbotScore.BAD        | BAD = 3        |

</details>

<details>

<summary>Add a Reputation Script to an indicator type</summary>

1. Go to Settings → Configurations → Object Setup → Indicators → **Types**.
2. Select the indicator type and click **Edit**.
3.  Select the relevant reputation script.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Reputation scripts must have the <strong>reputation</strong> tag applied to appear in the list.</p></div>

</details>

<details>

<summary>Run a Reputation Script in the CLI</summary>

You can run out-of-the-box or custom reputation scripts in the CLI to set the verdict for a specific indicator.

The following are examples for running the out-of-the-box `CertificateReputation` and `MalicioiusRationReputation` reputation scripts in the CLI.

* `!CertificateReputation input=<value of the indicator>`
* `!MalicioiusRationReputation input=<value of the indicator>`

</details>
