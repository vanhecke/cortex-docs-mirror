# Cloud Security Command Center permissions

Controls the ability to view and edit the Cortex Cloud Command Center, which is the central command center for cloud security, and includes capabilities like Cloud Security Posture Management (CSPM), Application Security Posture Management (ASPM), and Data Security Posture Management (DSPM).

{% hint style="info" %}
### Notice

Requires a Cloud Runtime Security, Cloud Posture Security, or Cortex XSIAM Premium license.
{% endhint %}

For more information, see [Cortex Cloud Command Center](../../../detect-investigate-and-respond-to-threats/monitor-dashboards-and-reports/dashboard-reference/command-center-reference/cortex-cloud-command-center).

| Permission | Description                                                                                                                                                                                                                                                                                                                                                   | Roles Example                                                                         |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| None       | No access to the Cloud Security Command Center.                                                                                                                                                                                                                                                                                                               | Most roles, unless they need Cloud Security.                                          |
| View       | Read-only access to the Cloud Security Command Center.                                                                                                                                                                                                                                                                                                        | Cloud viewer roles, such as Data Security Viewer, Developer, and AppSec Admin.        |
| View/Edit  | <p>Enables access and filtering, but it does not allow for editing the structure or widgets of the dashboard itself, as these are predefined.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>You also need Dashboards <strong>Enabled</strong> to view/edit these dashboards.</p></div> | Cloud admin roles, such as AI Security Administrator and Data Security Administrator. |

### Required and recommended permissions

As this dashboard aggregates data from complex cloud inventories, it will not populate correctly unless the following permissions are also granted:

| Permission                | Permission Level | Reason                                                                                            |
| ------------------------- | ---------------- | ------------------------------------------------------------------------------------------------- |
| Dashboards                | Enabled          | Required for the dashboard.                                                                       |
| Command Center Dashboards | View             | Cloud security cases and issues require this for click-through and context. Strongly recommended: |
| Asset Inventory           | View             | Cloud asset data requires this permission for full visibility. View: Strongly recommended:        |
| Graph Search              | View             | Cloud asset relationship visualization enhances cloud security context. Recommended.              |
