---
description: >-
  Format indicator data for DBot to ingest information about indicators to
  determine if they are malicious.
---

# Reputation and DBot score

DBot is the Cortex XSIAM machine learning bot, which ingests information about indicators to determine if they are malicious. Since DBot requires a very specific dataset, you must format the data as follows. As described in [Generic reputation commands](../generic-commands#UUID-67e7ba5f-4f74-45fc-8f2f-1aab4ef77100), when developing an integration that implements a generic reputation command, it is necessary also to create a corresponding DBot score object.

**Context format**

```programlisting
"DBotScore": {
  "Indicator" : "foo@demi.com",
  "Type": "email",
  "Vendor": "JoeSecurity",
  "Score": 3,
  "Reliability": "A - Completely reliable"
} 
```

The DBot score must be at the root level of the context and contain all the following required keys.

| Key         | Meaning                                                                                                            | Required? |
| ----------- | ------------------------------------------------------------------------------------------------------------------ | --------- |
| Indicator   | The indicator value.                                                                                               | Yes       |
| Type        | The indicator type. Can be: ip, file, email, url, cve, account, cider, domainglob, certificate, or cryptocurrency. | Yes       |
| Vendor      | The vendor reporting the score of the indicator.                                                                   | Yes       |
| Score       | An integer regarding the status of the indicator. See Score Types below.                                           | Yes       |
| Reliability | The reliability of the source providing the intelligence data. See Reliability Level below.                        | Yes       |
| Message     | Optional message to show an API response. For example, `Not found`.                                                | Optional  |

**Reliability level**

When merging indicators, the reliability of an intelligence data source influences the reputation of an indicator and the values assigned to indicator fields. An integration that outputs a DBotScore object and defines each indicator's reliability should allow the user to manually configure the default reliability for the created indicator's DBot Score. This is done by implementing a `Source Reliability` parameter (named `integration_reliability`) in the YAML file. This parameters is later used to determine the reliability level when creating the DBotScore object. &#x20;

**Example of implementing a reliability parameter in an integration YAML file**

```programlisting
- name: integration_reliability
  display: Source Reliability
  additionalinfo: Reliability of the source providing the intelligence data.
  defaultvalue: C - Fairly reliable
  options:
  - A+ - 3rd party enrichment
  - A - Completely reliable
  - B - Usually reliable
  - C - Fairly reliable
  - D - Not usually reliable
  - E - Unreliable
  - F - Reliability cannot be judged
  required: true
  type: 15
```

{% hint style="info" %}
### Note

The values are case sensitive.
{% endhint %}

**Score values**

DBot uses an integer to represent the reputation of an indicator.

| Number | Reputation |
| ------ | ---------- |
| 0      | Unknown    |
| 1      | Benign     |
| 2      | Suspicious |
| 3      | Malicious  |

**Unknown**

An unknown score can be interpreted in the following ways:

* The vendor returns an `Unknown` score for the indicator.
* The vendor returns nothing on the indicator.

**Malicious**

If the DBot score is returned as a `3` or `Malicious`, you need to add to the context that a malicious indicator was found. To do this, add an additional key to the `URL`, `IP`, or `File` context called `Malicious` as follows:

```programlisting
demisto.results({
     "Type": entryTypes["note"],
     "EntryContext": {
        "URL": {
            "Data": "STRING, The URL",
            "Malicious": {
                "Vendor": "STRING, Vendor reporting the malicious status",
                "Description": "STRING, Description of the malicious url"
            }
        },
         "File": {
            " SHA1/MD5/SHA256": "STRING, The File Hash",
            "Malicious": {
                "Vendor": "STRING, Vendor reporting the malicious status",
                "Description": "STRING, Description of the malicious hash"
            }
        },
         "IP": {
            "Address": "STRING, The IP",
            "Malicious":{
                "Vendor": "STRING, Vendor reporting malicious",
                "Description": "STRING, Description about why IP was determined malicious"
        },
        },
         "Domain": {
            "Name": "STRING, The Domain",
            "Malicious": {
                "Vendor": "STRING, Vendor reporting the malicious status",
                "Description": "STRING, Description of the malicious domain"
            }
        }
    }
})
```

Malicious has two key values: `Vendor` and `Description`. The vendor is the entity reporting the malicious indicator. The description explains briefly what was found. For example:

```programlisting
"URL": {
    "Data": "http://viruswarehouse.com",
    "Malicious": {
        "Vendor": "VirusTotal",
        "Description": "Wannacry ransomware detected"
    }
}
```

{% hint style="info" %}
### Note

It is not possible to use the Cortex XSIAM Transformers (DT) within the DBot score context. For example, using the following in your DBot context, will not work:

```programlisting
DBotScore(val.Indicator == obj.Indicator)
```
{% endhint %}
