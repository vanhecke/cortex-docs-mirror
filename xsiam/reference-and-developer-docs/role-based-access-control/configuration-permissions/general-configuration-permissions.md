# General Configuration permissions

Controls access to core platform settings that affect system-wide behavior, such as server settings, timezone settings, and system preferences. Access these through **Settings** → **Configurations** → **General** → **Server Settings**.

For more information, see [Configure server settings](../../../onboard-cortex-xsiam/post-deployment/configure-server-settings).

| Permission | Description                                                                     | Roles Example                                                                                                                                                                                                                                                                    |
| ---------- | ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to the **Server Settings** page, apart from Keyboard Shortcuts.       | <ul><li>SOC Tier-1 Analyst: No need to access or modify server configuration.</li><li>Threat Hunter: Server configuration is not typically relevant to threat hunting.</li></ul>                                                                                                 |
| View       | Read-only access to the **Server Settings** page.                               | <ul><li>SOC Tier-2 Analyst: May need View for troubleshooting context.</li><li>SOC Tier-3 Analyst: May need to understand system configuration during investigations.</li><li>Security Engineer: Should understand configuration, but changes should go through Admin.</li></ul> |
| View/Edit  | Full access to modify server and retention settings on the **Server Settings**. |                                                                                                                                                                                                                                                                                  |

### Required and recommended permissions

Consider adding the following permissions:

| Permission               | Permission Level | Reason                                                                                                    |
| ------------------------ | ---------------- | --------------------------------------------------------------------------------------------------------- |
| Auditing                 | View             | Track all configuration changes for compliance and change management. Strongly recommended.               |
| Access Management        | View             | Understand user access context when configuring system-wide settings. Strongly recommended.               |
| Alert Notifications      | View             | Notification settings may be affected by general configuration changes. Recommended.                      |
| Cases & Issues           | View             | Understand how configuration changes impact alert processing. Recommended.                                |
| Broker Service           | View             | General settings may affect the behavior of the Broker VM and data collection. Recommended.               |
| Dashboards               | Enabled          | View system health dashboards affected by configuration changes. Recommended.                             |
| Query Center             | View             | Query system data to validate configuration changes. Recommended.                                         |
| Exception Approver Admin | View/Edit        | Users who configure server settings may also need to configure exception approval workflows. Recommended. |
