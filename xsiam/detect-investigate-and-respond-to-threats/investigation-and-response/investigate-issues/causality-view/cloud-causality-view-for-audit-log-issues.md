---
description: >-
  Investigate cloud audit log issues in Cortex XSIAM with the cloud causality
  view.
---

# Cloud causality view for audit log issues

The Cloud causality view presents entity context directly within Cortex XSIAM issues, enabling security analysts to triage and scope cloud incidents in a single location. It displays the following context for a cloud audit log issue:

* Caller IP and network intelligence: The network origin, scope, and reputation of the action.
* Identity information: The acting identity profile, authentication behavior, and access privileges.
* Target cloud asset details: Identifies the specific cloud asset(s) affected by this issue.

In this context, you can see who acted, how the identity was authenticated, what the identity accessed, and where the action originated, without switching tools.

The Cloud causality view shows cloud audit log issues as a source-to-destination graph, linking the identity or caller IP that initiated an action to the affected cloud asset. Cortex XSIAM surfaces this context directly in the UAI by consolidating provider audit logs (Amazon Web Services CloudTrail, Microsoft Azure Activity Logs, and Google Cloud Platform Audit Logs).

The Cloud causality view presents cloud context for investigation and does not modify cloud provider configuration. From a case, drill down to a cloud audit log issue to open the Cloud causality view for that issue.

{% hint style="info" %}
When the UAI does not resolve an asset for an identity or a cloud resource, the Cloud causality view derives the displayed name from the cloud audit log.
{% endhint %}

#### Use cases

* Investigate the identity behind a cloud action: Select the identity node in the Cloud causality view to determine who performed the action and how the identity authenticated, and drill down to the identity name, identity type, cloud provider, and the identity that invoked the action.
* Trace the origin of a cloud action: Select the caller IP node in the Cloud causality view to establish where the action originated, and drill down to the caller IP address, autonomous system number, and geolocation.
* Assess the impact on a cloud resource: Select the destination node in the Cloud causality view to identify the affected cloud resource, and drill down to the resource name, referenced resource ID, resource type, and resource subtype.
* Focus the investigation on a single entity: Select a node in the Cloud causality view to filter the bottom table to the issues related to the selected node, and review the related events with fields such as timestamp, cloud provider, project, region, identity name, and identity type.
* Pivot to the full asset record: For an identity or a cloud resource that resolves to a Unified Assets Inventory (UAI) asset, open the asset card from the node to investigate the asset across the inventory, and review the identity and target cloud asset as the affected assets of the issue.

#### Supported platforms

The Cloud causality view supports cloud audit log issues and cases from the following cloud providers:

* Amazon Web Services
* Microsoft Azure
* Google Cloud Platform

#### User roles and permissions

The Cloud causality view is available to users whose role grants access to issues and to cloud audit log data.

### Node types

Each node type displays relevant details for your investigation, all conveniently accessible within a single window.

The Cloud causality view provides the caller IP node, identity node, and the destination node.

<details>

<summary>Caller IP node</summary>

Select the caller IP node in the Cloud causality view to display the caller IP overview in the left panel. The caller IP overview establishes where the action originated.

The caller IP overview includes the following information.

<table><thead><tr><th width="183">Field</th><th>Description</th></tr></thead><tbody><tr><td>Caller IP</td><td>Identifies the source IP address that acted.</td></tr><tr><td>Caller IP ASN</td><td>Specifies the autonomous system number associated with the caller IP address.</td></tr><tr><td>Caller IP geolocation</td><td>Indicates the geographic location associated with the caller IP address.</td></tr></tbody></table>

</details>

<details>

<summary>Identity node</summary>

Select the identity node in the Cloud causality view to display the identity overview in the left panel. The identity overview presents the acting identity and the identity that invoked the action, so you can determine the actor and the authentication context in a single view.

The identity overview includes the following information.

<table><thead><tr><th width="196">Field</th><th>Description</th></tr></thead><tbody><tr><td>Identity name</td><td>Specifies the human-readable identifier used to track the identity across cloud audit logs.</td></tr><tr><td>Identity type</td><td>Indicates the nature of the identity: <code>User</code>, <code>Service</code>, or <code>Resource</code>.</td></tr><tr><td>Identity sub type</td><td>Defines the provider-specific classification of the identity</td></tr><tr><td>Cloud provider</td><td>Identifies the ecosystem where the identity is defined and managed, such as Amazon Web Services, Google Cloud Platform, Microsoft Azure, or Oracle Cloud Infrastructure.</td></tr><tr><td>Identity invoke by name</td><td>Displays the name of the identity that invoked the action.</td></tr><tr><td>Identity invoke by type</td><td>Indicates the type of identity that invoked the action.</td></tr><tr><td>Identity invoked by sub type</td><td>Specifies the subtype of the identity that invoked the action.</td></tr><tr><td>User agent</td><td>Details the client and operating system family used to act.</td></tr></tbody></table>

{% hint style="info" %}
Additional identity context, such as administrative privilege and multi-factor authentication status, is sourced from the UAI and is available when a UAI asset resolves for the identity.
{% endhint %}

</details>

<details>

<summary>Destination node</summary>

Select the destination node in the Cloud causality view to display the target cloud asset overview in the left panel. The destination node represents the cloud resource affected by the action, so you assess the impact of the issue or case without opening the cloud inventory.

The target cloud asset overview includes the following information.

<table><thead><tr><th width="181">Field</th><th>Description</th></tr></thead><tbody><tr><td>Resource name</td><td>Displays the name of the affected cloud resource.</td></tr><tr><td>Referenced resource ID</td><td>Identifies the cloud provider identifier of the affected resource.</td></tr><tr><td>Resource type</td><td>Indicates the category of the affected cloud resource.</td></tr><tr><td>Resource sub type</td><td>Defines the provider-specific classification of the affected cloud resource.</td></tr></tbody></table>

{% hint style="info" %}
When a UAI asset resolves for the source or destination node, the Cloud causality view displays the UAI panel for that node.
{% endhint %}

</details>

#### All events table

Select a node in the Cloud causality view to filter the bottom table to the issues related to the selected node. Cancel the node selection to return the bottom table to the unfiltered view.

#### UAI connection

When an identity or a target cloud asset in a cloud audit log issue resolves to an asset in the Unified Assets Inventory (UAI), the Cloud causality view connects the node to that asset. The connection aligns the investigation view with the inventory, so you access the complete asset record without searching the inventory separately. The Cloud causality view connects a node only when the identity or the target cloud asset resolves to an existing UAI asset, and the connection provides navigation and context for investigation without creating or modifying UAI assets.

The Cloud causality view provides the following connections for a node that resolves to a UAI asset:

* **Node name**: The node displays the name recorded in the UAI, so the entity in the Cloud causality view matches the entity in the inventory.
* **Asset details**: Selecting the node displays the UAI details for the asset in the left panel.
* **Asset card**: Right-clicking the node and selecting the **Open Asset Card** action opens the asset card for the corresponding UAI asset.

For an issue, the identity and target cloud asset that resolve to UAI assets are recorded as the affected assets of the issue and link to the corresponding UAI assets.

{% hint style="info" %}
When the UAI does not resolve an asset for a node, the node displays the name derived from the cloud audit log and does not link to a UAI asset.
{% endhint %}
