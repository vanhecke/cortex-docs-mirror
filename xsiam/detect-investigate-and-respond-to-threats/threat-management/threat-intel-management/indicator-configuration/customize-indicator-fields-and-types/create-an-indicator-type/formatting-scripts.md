---
description: Use formatting scripts to normalize indicator values before storage.
---

# Formatting scripts

A formatting script has the following main functions:

* Validate inputs, for example, to check that the top-level domain (TLD) is valid.
* Modify how the indicator appears in Cortex XSIAM such as the War Room.

After indicator values are extracted according to the defined regex, the formatting script can be used to modify how the indicator value appears in the War Room and reports. For example, the IP indicator type uses the **`UnEscapeIPs`** formatting script, which removes any defanged characters from an IP address, so **`127[.]0[.]0[.]1`** is formatted to **`127.0.0.1`**. When you click the IP address in the War Room, you see the formatted IP address. This extracted indicator value is then added to the Threat Intel database.

**Out-of-the-box Formatting Scripts**

You can create a new script, or you can use an out-of-the-box formatting script on the **Scripts** page, for example:

* **`UnEscapeIPs:`** Removes escaping characters from IP addresses. For example, 127\[.]0\[.]0\[.]1 transforms to 127.0.0.1.
* **`ExtractDomainAndFQDNFromUrlAndEmail:`** Extracts domains and FQDNs from URLs and emails, used by the Domain indicator. It removes prefixes such as proofpoint or safelinks, removes escaped URLs, and extracts the FQDN.
* **`ExtractEmailV2:`** Verifies that an email address is valid and only returns the address if it is valid.

<details>

<summary>Formatting Script example</summary>

In the following example, the RemoveEmpty script removes empty items, entries, or nodes from an array.

```programlisting
// pack version: 1.2.30
const EMPTY_TOKENS = argToList(args.empty_values);

function toBoolean(value) {
    if (typeof(value) === 'string') {
        if (['yes', 'true'].indexOf(value.toLowerCase()) != -1) {
            return true;
        } else if (['no', 'false'].indexOf(value.toLowerCase()) != -1) {
            return false;
        }
        throw 'Argument does not contain a valid boolean-like value';
    }
    return value ? true : false;
}

function isObject(o) {
    return o instanceof Object && !(o instanceof Array);
}

function isEmpty(v) {
    return (v === undefined) ||
           (v === null) ||
           (typeof(v) == 'string' && (!v || EMPTY_TOKENS.indexOf(v) !== -1)) ||
           (Array.isArray(v) && v.filter(x => !isEmpty(x)).length === 0) ||
           (isObject(v) && Object.keys(v).length === 0);
}

function removeEmptyProperties(obj) {
    Object.keys(obj).forEach(k => {
        var ov = obj[k];
        if (isObject(ov)) {
            removeEmptyProperties(ov);
        } else if (Array.isArray(ov)) {
            ov.forEach(av => isObject(av) && removeEmptyProperties(av));
            obj[k] = ov.filter(x => !isEmpty(x));
        }
        if (isEmpty(ov)) {
            delete obj[k];
        }
    });
}

var vals = Array.isArray(args.value) ? args.value : [args.value];

if (toBoolean(args.remove_keys)) {
    vals.forEach(v => isObject(v) && removeEmptyProperties(v));
}
return vals.filter(x => !isEmpty(x));
```

</details>

<details>

<summary>Formatting Script input</summary>

The formatting script requires a single input argument named **`input`** that accepts a single indicator value or an array of indicator values. The input argument should be an array to accept multiple inputs and return an entry-result per input.

| Argument    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`input`** | <p>Accepts a string or array of strings representing the indicator value(s) to be formatted. Will be accessed within the script using <strong><code>demisto.args().get(‘input’, [])</code></strong>.</p><p>In the script settings, the <strong>Is Array</strong> checkbox must be selected (see screenshot below).The script code must be able to handle a single indicator value (as string), multiple indicator values in CSV format (as string) and an array of single indicator values (array).</p> |

![formatting-8-input.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6d7a80b6055832b530659c0c1f59b357c9d696f6%2F1ce52f84db6ecc920741a0a5bc4de60aad9c6f6289f695df9f962b78d28ecde9.png?alt=media)

</details>

<details>

<summary>Formatting Script outputs</summary>

The indicators appear in a human-readable format in Cortex XSIAM. The output should be an array of formatted indicators or an array of entry results (an entry result per indicator to be created). The entry result per input can be a JSON array to create multiple indicators. If the entry result is an empty string, it is ignored and no indicator is created.

Use the `return_results` function to generate the script output. For more information, see [https://xsoar.pan.dev/docs/integrations/code-conventions#return\_results](https://xsoar.pan.dev/docs/integrations/code-conventions#return_results).

Single-value result:

```programlisting
results = CommandResults(
    outputs_prefix='VirusTotal.IP',
    outputs_key_field='Address',
    outputs={
        'Address': '8.8.8.8',
        'ASN': 12345
    }
)
return_results(results)
```

Multiple-value results:

```programlisting
results = [
    CommandResults(
        outputs_prefix='VirusTotal.IP',
        outputs_key_field='Address',
        outputs={
            'Address': '8.8.8.8',
            'ASN': 12345
        }
    ), 
    CommandResults(
        outputs_prefix='VirusTotal.IP',
        outputs_key_field='Address',
        outputs={
            'Address': '1.1.1.1',
            'ASN': 67890
        }
    )]
return_results(results)
```

</details>

<details>

<summary>Add a Formatting Script to an indicator type</summary>

1. Go toSettings → Configurations → Object Setup → Indicators → **Types**.
2. Select the indicator type and click **Edit**.
3.  Select the desired formatting script.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Formatting scripts must have the <strong><code>indicator-format</code></strong> tag to appear in the list.</p></div>

{% hint style="info" %}
### Note

Formatting scripts for out-of-the-box indicator types are system-level, which means that the formatting scripts for these indicator types are not configurable. To create a formatting script for an out-of-the-box indicator type, you need to disable the existing indicator type and create a new (custom) indicator type. If you configured a formatting script before this change and updated your content, this configuration reverts to content settings (empty).
{% endhint %}

</details>

<details>

<summary>Run a Formatting script in the CLI</summary>

You can run out-of-the-box or custom formatting scripts in the CLI to check the extracted indicator data is properly formatted.

The following are examples of the syntax for running the out-of-the-box `UnEscapeIPs` formatting script in the CLI.

* `!UnEscapeIPs !UnEscapeIPs input=127.0.0[.]1`
* `!UnEscapeIPs input=127.0.0[.]1,8.8.8[.]8`
* `!UnEscapeIPs input=${contextdata.indicators}` (where the key `contextdata.indicators` in the context object is an array)

</details>
