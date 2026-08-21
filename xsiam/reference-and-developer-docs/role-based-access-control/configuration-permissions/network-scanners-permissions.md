---
description: Manage access to Cortex XSIAM network scanner configuration and operations.
---

# Network Scanners permissions

Located under Settings → Configurations → Network Scanning, this permission allows administrators to set up scan definitions, manage credentials for authenticated scans, configure targets, and view results.

Requires either the ASM and the Exposure Management add-ons, or a Cortex XSIAM Premium license with the Exposure Management add-on.

For more information, see [Cortex Network Scanner](../../../detect-investigate-and-respond-to-threats/exposure-management/cortex-network-scanner).

While configured under Integrations, Network Scanners serve as the active discovery engine for the broader vulnerability lifecycle. Data generated here directly populates the Vulnerability Management and Exposure Management modules.

| Permission | Description                                                                                               | Role Example                                                                                               |
| ---------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| None       | Users cannot access the Network Scanners page.                                                            | SOC Tier-1 and 2 Analysts: No scanning responsibilities.                                                   |
| View       | Users can view existing scanner configurations and scan results, but cannot create, run, or modify scans. | <ul><li>SOC Tier-3 Analyst: Review scan configurations.</li><li>Threat Hunter: Review scan data.</li></ul> |
| View/Edit  | Full control to create, configure, run, and delete network scan configurations                            | Security Engineer: Configure vulnerability scanning.                                                       |

#### Required and recommended permissions

Vulnerability scanning is deeply integrated with asset discovery and infrastructure. Consider adding the following permissions:

| Permission                                   | Permission Level  | Reason                                                                                                        |
| -------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------- |
| Vulnerability Testing (under Attack Surface) | View or View/Edit | Core permission to access Network Scanners pages. Required.                                                   |
| Credentials                                  | View/Edit         | Strongly recommended to manage scan authentication credentials used for authenticated vulnerability scanning. |
| Broker Service                               | View/Edit         | Required if using Broker VM as the scanning infrastructure.                                                   |
| Cases & Issues                               | View              | Recommended to view vulnerability-related cases and issues generated from scan results.                       |
| Query Center                                 | View              | Recommended to query scan results and vulnerability data via XQL.                                             |
