---
description: Configure Application Security configuration permissions in Cortex XSIAM.
---

# Configurations - Application Security permissions

Application Security Configurations controls access to the Application Security settings under **Settings** → **Configurations** → **Application Security**, which includes the following:

* Application Configuration: Controls SLA target settings (Critical, High, Medium, Low severity target days and approaching SLA threshold), and the auto-refresh toggle for related application assets.
* AppSec Issues Configuration: Controls whether SBOM (Software Bill of Materials) findings are treated as new vulnerabilities. When enabled, all detected SBOM findings are treated as new vulnerabilities. When disabled, the baseline for identifying new SBOM vulnerabilities starts with the next scan, excluding previously identified findings.

{% hint style="info" %}
### License

Requires the Application Security add-on in addition to Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license.
{% endhint %}

| Permission | Description                                                                 | Roles Example                                                                                                                                                                                      |
| ---------- | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to Application Security configuration pages.                      | <ul><li>SOC Tier-1, 2, and 3 Analysts: AppSec configuration is not part of the primary SOC workflow.</li><li>Threat Hunter: AppSec configuration is outside the scope of threat hunting.</li></ul> |
| View/Edit  | Full access to view and modify Application Security configuration settings. | Security Engineer: May need to configure SLA targets and SBOM behavior as part of AppSec posture management.                                                                                       |

**Required and recommended permissions**

To understand the impact of modifying SLA targets and SBOM baselines, administrators should have visibility into the actual AppSec issues queues and the related application assets these settings affect.

| Permission                  | Permission Level | Reason                                                                                                                                                                                                                                                                    |
| --------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application Security Issues | View             | Strongly Recommended. Configurations made on this page directly dictate how SBOM findings appear and how SLA deadlines are calculated. Access to the Issues queue allows administrators to verify that their configuration changes produce the desired tracking behavior. |
| Asset Inventory             | View             | Recommended. The configurations include an auto-refresh toggle for related application assets. Asset Inventory visibility helps administrators understand which assets are being affected by this setting.                                                                |
