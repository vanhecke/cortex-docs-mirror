---
description: Select resolution reasons when closing cases and issues in Cortex XSIAM.
---

# Resolution reasons for cases and issues

When you resolve a case or issue, you must also specify a resolution reason. The following table describes the resolution reasons for selection in Cortex XSIAM.

{% hint style="info" %}
### Note

The displayed resolution reasons are domain-specific. You can see the resolution reasons that are defined for a domain under **Configurations** → **Object Setup** → **Cases** → **Domains**.
{% endhint %}

<table><thead><tr><th width="226">Resolution reason</th><th>Description</th></tr></thead><tbody><tr><td>Resolved - True Positive</td><td><p>The case or issue was correctly identified as a real threat, and the case was successfully handled and resolved.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Cases and issues resolved as True Positive and False Positive help to identify real threats in your environment by comparing future cases and associated issues to the resolved cases. Therefore, the handling and scoring of future cases is affected by these resolutions.</p></div></td></tr><tr><td>Resolved - False Positive</td><td><p>The case or issue is not a real threat.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Cases and issues resolved as True Positive and False Positive help to identify real threats in your environment by comparing future cases and associated issues to the resolved cases. Therefore, the handling and scoring of future cases is affected by these resolutions.</p></div></td></tr><tr><td>Resolved - Security Testing</td><td>The case or issue is related to security testing or simulation activity, such as a BAS, pentest, or red team activity.</td></tr><tr><td>Resolved - Known Issue</td><td>The case or issue is related to an existing issue or an issue that is already being handled.</td></tr><tr><td>Resolved - Duplicate Case</td><td>The case or issue is a duplicate of another case.</td></tr><tr><td>Resolved - Risk Accepted</td><td>The case or issue is related to a known mitigation or impact.</td></tr></tbody></table>

If you created a custom resolution, it is also available for selection.
