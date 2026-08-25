---
description: >-
  Review Cortex XSIAM assessment results and generate or schedule downloadable
  compliance reports.
---

# View and manage compliance assessments and reports

Create a compliance assessment report based on a Cortex compliance standard for immediate viewing or download, or schedule recurring reports to continue monitoring compliance over time.

## What are compliance assessments and reports?

A compliance assessment provides you with a consolidated view of your organization's compliance with a selected standard. Compliance status is automatically updated in the **Assessments** results page for you to view.

{% hint style="info" %}
**NOTE**

Compliance assessment results may take up to six hours to be generated.
{% endhint %}

When you configure your assessment profile, you can generate PDF or CSV reports and optionally receive them via email. You can also view a list of compliance reports and download them from the **Reports** page.

## Compliance score

The compliance score represents the percentage of individual controls assessed against individual assets that adhere to the prescribed requirements. This score is calculated based on the ratio of controls in a passed status to the total number of controls assessed against a scope of assets.

By providing this high-level score based upon the granular controls performance, the platform enables you to quickly gauge your organization's overall compliance posture and identify which controls require immediate attention to mitigate security risks.

{% hint style="info" %}
**NOTE**

The status of controls is determined by the evaluation of the associated rules. If an asset fails a check against any rule associated with a control, that control is considered failed for that asset.
{% endhint %}

### Control statuses

The compliance scoring system evaluates assets against assessment rules and assigns one of three statuses:

* _**Passed**_: Asset meets compliance requirements
* _**Failed**_: Asset does not meet compliance requirements
* _**Not Assessed**_: Asset was not evaluated against this control

### How compliance score is calculated

The formula for compliance score calculation is:

_**Compliance score = Passed Controls / (Passed Controls + Failed Controls) \* 100%**_

The score is rounded up to the next whole digit and expressed as a percentage.

This formula is applied consistently across each of the four scoring levels: rule, control, category, and standard, and across all asset scopes.

### Example compliance score calculation

Consider two assets A1 and A2, both assessed against two controls. While A1 passes both controls, A2 passes one control and fails one control.

The compliance score is calculated as follows:

_3 passed controls / (3 passed controls + 1 failed control) \* 100% = .75 \* 100% = 75%_
