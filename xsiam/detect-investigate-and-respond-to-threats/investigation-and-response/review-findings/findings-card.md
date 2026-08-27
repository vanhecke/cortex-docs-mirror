---
description: View selected finding details and investigation context in Cortex XSIAM.
---

# Findings card

The Findings card displays information about the selected finding. On this card you can see the following information.

{% hint style="info" %}
### Note

The information in this card is context specific, therefore some sections are not available for all findings.
{% endhint %}

<table><thead><tr><th width="160">Section</th><th>Description</th></tr></thead><tbody><tr><td>Header</td><td>Finding ID, name, category (such as, Vulnerability or Compliance), time created, and time updated.</td></tr><tr><td>Description</td><td>Reason that the finding was created.</td></tr><tr><td>Impact</td><td>Information about the possible impact of the finding on your system.</td></tr><tr><td>Asset</td><td><p>Name and type of the affected asset.</p><p>To investigate the asset, click on the asset name to open a new tab displaying the asset card.</p></td></tr><tr><td>Detection logic</td><td>Detection rule that identified the specific security risk, configuration gap, or malicious behavior generating the finding.</td></tr><tr><td>Compliance</td><td><p>Violated compliance standards and specific framework controls associated with the finding.</p><p>Click the expand icon to see a list of all standards associated with the finding and a granular breakdown of specific controls breached under each standard.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>License Note</strong></p><p>Requires Cortex XSIAM Premium or the Cortex Cloud Posture Management or Cortex Cloud Runtime Security add-on.</p></div></td></tr><tr><td>Evidence</td><td>Visualization of the finding in your environment.</td></tr><tr><td>Data</td><td>Normalized finding data.</td></tr></tbody></table>
