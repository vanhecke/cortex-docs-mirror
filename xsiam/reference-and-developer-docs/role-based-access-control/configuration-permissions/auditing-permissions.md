# Auditing permissions

Provides access to view audit logs that track all administrative and operational activities within Cortex XSIAM:

* Management Audit Logs: Track user actions, role modifications, and administrative operations. Go to **Settings** → **Management Audit Logs**.
* Agent Audit Logs: Track endpoint agent activities and related activities. Go to **Settings** → **Agent Audit Logs**.
* XDR Collector Audit Logs: Track XDR collector activities and data collection events. Go to **Settings** → **XDR Collector Audit Logs**.

{% hint style="warning" %}
### Caution

The Auditing module is intentionally restricted to View-only access. Audit logs are immutable records designed to maintain compliance and forensic integrity. They cannot be modified or deleted by any user.
{% endhint %}

| Permission | Description                                                                                                                                                                                                  | Roles Example                                                                                                                                                                                                                     |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | No access to any audit logs.                                                                                                                                                                                 | SOC Tier-1 Analyst: No Need for visibility into system activities, unless context is required.                                                                                                                                    |
| View       | <p>Read-only access to all audit log data.</p><p>Auditing is intentionally view-only. Audit logs are immutable records that cannot be modified or deleted to maintain compliance and forensic integrity.</p> | <ul><li>SOC Tier-2 and 3 Analysts, and Threat Hunters: Required for case investigation and understanding event timelines.</li><li>Security Engineer: Required for troubleshooting and validating configuration changes.</li></ul> |

### Required and recommended permissions

Consider adding the following permissions:

| Permission            | Permission Level | Reason                                                                                    |
| --------------------- | ---------------- | ----------------------------------------------------------------------------------------- |
| Cases & Issues        | View             | Provides context for audit events related to cases. Strongly recommended.                 |
| Query Center          | View             | Enables XQL queries against audit datasets. Strongly recommended.                         |
| Dashboards            | Enabled          | View audit-related dashboards for operational visibility. Recommended.                    |
| Agent Administrations | View             | Understand agent-related audit events in the context of endpoint management. Recommended. |
| Host Insights         | View             | Correlate audit events with host-level context and asset information. Recommended.        |
