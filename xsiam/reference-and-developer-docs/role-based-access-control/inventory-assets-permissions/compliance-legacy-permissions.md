# Compliance (Legacy) permissions

Cloud Compliance (Legacy) under **Inventory** → **Endpoints** → **Cloud Compliance** provides a read-only view of CIS benchmark compliance violations for cloud assets.

{% hint style="info" %}
### Notice

Requires a Cortex XSIAM Enterprise Plus license. If you have a Cloud Posture Security, Cloud Runtime Security, or Cortex XSIAM Premium license, see [Compliance - Cloud permissions](../cloud-security-and-posture-management-permissions/compliance-cloud-permissions).
{% endhint %}

| Permissions | Description                                                              | Roles Example                                                                                                                                                                     |
| ----------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None        | Cannot view the Compliance menu or any related pages.                    | SOC Tier-1 Analyst and Threat Hunter: Compliance monitoring is not part of daily triage/relevant to threat hunting.                                                               |
| View        | Read-only permission to view CIS compliance violations for Cloud assets. | <ul><li>SOC Tier-2 and 3 Analysts: May reference compliance status/data during investigations/advanced analysis.</li><li>Security Engineer: Monitor compliance posture.</li></ul> |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission      | Permission Level | Reason                                                                   |
| --------------- | ---------------- | ------------------------------------------------------------------------ |
| Asset Inventory | View             | Highly recommended to view assets associated with compliance violations. |
| Host Insights   | View             | Highly recommended to view endpoint details for the compliance context.  |
| Dashboards      | Enabled          | Enabled: Recommended to view endpoint details for compliance context.    |
| Query Center    | View             | Recommended to run XQL queries on network data.                          |
