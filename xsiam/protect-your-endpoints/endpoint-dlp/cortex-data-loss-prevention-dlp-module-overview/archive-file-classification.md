# Archive file classification

{% hint style="info" %}
**Note**:

Available from Cortex agent 9.3.
{% endhint %}

Archive file classification allows Cortex Data Loss Prevention (DLP) to inspect the contents of archive files (even if compressed). By applying your data-in-motion rules to the files inside, DLP ensures sensitive data remains protected even when packaged in an archive.

### **How it works**

* **Archive-Level Enforcement**: DLP evaluates the archive as a single entity. If any supported file within the archive matches a data profile in a data-in-motion rule, the rule's designated action (**Block**, **Report**, or **Allow**) is applied to the entire archive. Files inside the archive are not enforced individually.
* **Deep Inspection**: DLP inspects nested archives up to 50 levels deep. There is no limit on folder depth within the archive.
* **Unsupported Files**: Any files inside the archive that are not supported for classification are safely skipped and do not impact the overall result.

### **Supported archive formats**

Archive file classification supports common archive formats that vary between operating systems. For a complete list of supported file types, refer to the [Supported files](..#supported-file-types-and-extensions) documentation.

{% hint style="info" %}
**Note**:

Archive inspection is subject to standard file size constraints. The total archive size must remain within the maximum supported file size detailed in the Agent side limitations.
{% endhint %}

### **Partial classification**

Archives support partial classification. If DLP cannot fully scan an archive, for example, if the inspection times out, it will still enforce data-in-motion rules based on the contents it successfully classified.

* If a match is found in the scanned portion, DLP applies the matched main action.
* If no rule matches the scanned contents, DLP applies the default action defined in your endpoint DLP settings.
* If the archive is password-protected, it can still match data profiles that use the password-protected filter.
