# Network Configuration permissions

Network Configuration (**Inventory** → **Assets** → **Network Configuration**) enables administrators to define and manage the organization's network topology, such as internal and external IP address ranges, internal domain suffixes, and trusted networks.

{% hint style="info" %}
### Notice

External IP address ranges: Requires an ASM or Cortex XSIAM Premium license.

Trusted Networks: Requires a Cloud Posture Security or Cortex XSIAM Premium license.
{% endhint %}

Network topology configuration is frequently shared between the Security and IT Infrastructure teams. Ensure proper coordination before altering IP ranges or trusted network definitions.

For more information, see [Network configurations](../../../detect-investigate-and-respond-to-threats/asset-management/asset-configurations/network-configuration).

The Network Configuration permission controls the ability to view, create, and edit network topologies, IP ranges, and trusted domains.

| Permissions | Description                                                                                                   | Roles Example                                                                               |
| ----------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| None        | No access to the Network Configuration menu, IP ranges, internal domains, or trusted networks.                | SOC Tier-1 Analyst: Does not need access to network configuration.                          |
| View        | Read-only access to view defined IP ranges, internal domains, and trusted networks.                           | SOC Tier-2 and 3 Analysts, and Threat Hunters: Do not need access to network configuration. |
| View/Edit   | Full access to add, edit, and delete IP address ranges, internal domains, and trusted network configurations. | Security Engineer: Responsible for maintaining network configuration.                       |

**Required and recommended permissions**

Consider adding the following permissions:

| Category              | Permissions | Reason                                                                                         |
| --------------------- | ----------- | ---------------------------------------------------------------------------------------------- |
| Asset Inventory       | View        | Strongly recommended to view assets associated with IP ranges. View/Edit for Asset Management. |
| Agent Administrations | View        | Recommended for endpoint details linked to network ranges.                                     |
| Query Center          | View        | Recommended to run XQL queries on network data.                                                |
