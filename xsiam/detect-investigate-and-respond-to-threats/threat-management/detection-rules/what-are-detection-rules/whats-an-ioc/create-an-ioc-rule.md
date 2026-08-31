---
description: Create Cortex XSIAM IOC rules to generate issues from known threat indicators.
---

# Create an IOC rule

Create new indicator of compromise (IOC) rules and optionally define rule expiration for all IOC rules. You can create an IOC rule either by configuring a single one or by uploading a file that contains multiple IOCs.

{% hint style="info" %}
### Note

To ensure your IOC rules generate issues efficiently and do not overcrowd your Issues table, Cortex XSIAM automatically does the following:

* Disables any IOC rules that reach 5000 or more hits over 24 hours.
* Creates a rule exception based on the PROCESS SHA256 field for IOC rules that hit more than 100 endpoints over 72 hours.

If you have the Threat Intel Management add-on included in your license, create an indicator detection rule for File, Domain, and IP Address indicators rather than creating an IOC. For more information, see [Generate issues from indicators using indicator rules for prevention and detection](../../../threat-intel-management/indicator-configuration/generate-issues-from-indicators-using-indicator-rules-for-prevention-and-detection).
{% endhint %}

1. In **Threat Management** → **Detection Rules** → **IOC**, select **+ Add IOC**.
2. Configure the IOC criteria.

<details>

<summary>Configure a single IOC</summary>

**Configure a single IOC**

After investigating a threat, if you identify a malicious artifact, you can generate an issue for the **Single IOC** right away.

1. Configure the **INDICATOR** value on which you want to match.
2. Configure the IOC **TYPE**. Options are **Full Path**, **File Name**, **Domain**, **Destination IP**, and MD5 or SHA256 **Hash**.
3. Configure the **SEVERITY** you want to associate with the issue for the IOC.
4. (Optional) Enter a comment that describes the IOC.
5. (Optional) Configure the IOC's **REPUTATION** and its **RELIABILITY**.
6. (Optional) Configure the **EXPIRATION** settings for this IOC. **Default**, **Specific Expiration Date**, **No Expiration**.
7. Click **Save**.

</details>

<details>

<summary>Upload multiple IOCs</summary>

**Upload multiple IOCs**

If you want to match multiple indicators, you can upload the criteria in a CSV file. You can upload IOCs using REST APIs in either CSV or JSON format.

Upload a file, one IOC per line, that contains up to 20,000 IOCs. For example, you can upload multiple file paths and MD5 hashes for an IOC rule. To help you format the upload file in the syntax that Cortex XSIAM accepts, you can download the example file.

1. Select **Upload File**.
2.  Drag and drop the CSV file containing the IOC criteria in the drop area of the **Upload File** dialog or **Browse** for the file.

    Cortex XSIAM supports files with multiple IOCs in a pre-configured format. For help in determining the format syntax, download the example text file.
3. Configure the **SEVERITY** you want to associate with the issue for the IOCs.
4. Define the **DATA FORMAT** of the IOCs in the CSV file. Options are **Mixed**, **Full Path**, **File Name**, **Domain**, **Destination IP**, and MD5 or SHA256 **Hash**.
5. (Optional) Configure the IOC's **REPUTATION** and its **RELIABILITY**.
6. (Optional) Enter an **EXPIRATION** for the IOC. **Default**, **Specific Expiration Date**, **No Expiration**.
7. Click **Upload**.

</details>

3.  (Optional) Define any expiration criteria for your IOC rules.

    You can also configure additional expiration criteria per IOC type to apply to all IOC rules of that type. In most cases, IOC types like Destination IP or Host Name are considered malicious only for a short period of time since they are soon cleaned and then used by legitimate services, from which time they only cause false positives. For these types of IOCs, you can set a defined expiration period. The expiration criteria you define for an IOC type will apply to all existing rules and additional rules that you create in the future. By default, Cortex XSIAM does not apply an expiration date set on IOCs.

    1. Select **Default Rule Expiration**.
    2. Set the expiration for any relevant IOC type. Options are **Never, 7 Days, 30 days, 90 days**, or **180 days**.
    3. Click **Save**.
