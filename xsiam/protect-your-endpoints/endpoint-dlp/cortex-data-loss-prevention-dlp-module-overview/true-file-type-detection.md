# True-file type detection

When Cortex Data Loss Prevention (DLP) scans a file, true file-type detection identifies the file based on its actual internal format rather than relying on its file extension.&#x20;

This ensures consistent policy enforcement and prevents users from intentionally bypassing DLP rules by masking files.

* **Accurate Enforcement**: DLP recognizes the sensitive data inside the file and applies the matching data-in-motion rule, regardless of the file's current extension.
* **Evasion Prevention**: If a user renames a restricted document (for example, changing `report.pdf` to `report.log`), DLP still identifies the true file type as a PDF, scans the embedded sensitive data, and enforces the appropriate rule.

{% hint style="info" %}
Supported file scans on Windows and macOS
{% endhint %}

