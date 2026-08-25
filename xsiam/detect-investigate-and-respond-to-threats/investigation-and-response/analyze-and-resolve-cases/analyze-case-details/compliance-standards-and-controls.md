---
description: >-
  Review compliance standards and violated controls for Posture cases in Cortex
  XSIAM.
---

# Compliance standards and controls

{% hint style="info" %}
**License note**

Requires Cortex XSIAM Premium or the Cortex Cloud Posture Management or Cortex Cloud Runtime Security add-on.
{% endhint %}

For Posture cases, you can quickly evaluate regulatory impact and policy compliance by reviewing the compliance standards and violated controls associated with the case.

{% hint style="info" %}
**Tip**

While violated compliance controls can also be viewed within individual Issues and Findings cards, reviewing them in the Cases card provides a consolidated view of compliance impact across the entire incident story.
{% endhint %}

### View compliance details in a case

1. Open the Cases card and navigate to the **Entities & Frameworks** section.
2. Locate the **Compliance** subsection, which summarizes high-level compliance activity.
3. Click the expand icon to open the **Compliance** dialog.\
   The dialog displays:
   * Compliance Standards: A comprehensive list of all standards associated with the case (e.g., PCI-DSS, NIST SP 800-53, SOC 2, ISO 27001).
   * Violated Controls: A granular breakdown of specific controls breached under each standard.
4. To drill down into specific compliance findings, locate the relevant standard and control in the list and click **View issues** next to the control.\
   This automatically redirects you to the **Issues & Insights** tab in the **Detailed View**, pre-filtered to display only the issues matching the selected compliance standard and control.
