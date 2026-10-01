---
description: Map network events for Cortex XSIAM analytics.
---

# How to map network events for analytics

{% hint style="info" %}
**License**

To enable Identity Threat Detection and Response (ITDR) analytics, you must have the ITDR license and ingest identity logs. Full identity analytics capabilities are optimized for data collected via Cortex XDR agents and specific cloud/SaaS integrations.
{% endhint %}

To enable Cortex XSIAM to automatically create network stories and run network analytics, you must map traffic-between-endpoints events to a fixed set of Cortex Data Model (XDM) fields. If a mandatory field is missing, the event is dropped from the network story.

Once these network events are mapped, Cortex XSIAM provides out-of-the-box detection logic for third-party firewalls. For more information, see [Third-Party Firewalls](https://cortex-docs.paloaltonetworks.com/analytics-alerts/alerts-by-data-source/third-party-firewalls).

{% hint style="info" %}
**Note**

For technical conventions and implementation logic for complex authentication scenarios, see [Advanced network mapping: deep dives](../../../reference-and-developer-docs/reference/xdm-fields-for-mapping-network-events/advanced-network-mapping-deep-dives).
{% endhint %}

{% hint style="warning" %}
**Prerequisite**

* You must have **View/Edit** RBAC permissions for **Data Management** (under **Configurations > Data Management**).
* Familiarize yourself with the Cortex Data model (XDM) schema for field definitions and naming conventions, see [Cortex XSIAM Data Model Schema](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/).
{% endhint %}

<details>

<summary>Classification signals</summary>

Treat a log sample as a network event only if it carries a distinctive signal:

* **Traffic vocabulary**: Field names or values like `flow`, `traffic`, `connection`, `session`, `bytes_sent`, or `packets`.
* **Action values**: `allow`, `permit`, `deny`, `drop`, `block`, or `reset`.
* **Protocol names**: `tcp`, `udp`, `icmp`.
* **Transport 5-tuple**: The presence of both endpoint addresses, a port, and a protocol in one record.

</details>

<details>

<summary>Mapping principles</summary>

* **Map per record**: A single feed (like a firewall) may mix flows with admin commands and status logs. Only tag records as `NETWORK` if they supply a peer address.
* **Network is foundational**: Security judgments (IDS/IPS alerts, proxy decisions) should be mapped _on top of_ the network flow, not instead of it.
* **Preserve dual meaning**: An authentication event that carries a full transport flow (e.g., VPN login) should be tagged with BOTH `XDM_CONST.EVENT_TAG_AUTHENTICATION` and `XDM_CONST.EVENT_TAG_NETWORK`.

</details>

<details>

<summary>Mandatory XDM fields for network events</summary>

You must map all 17 mandatory fields to build network stories. For more detailed information on these fields, see [XDM fields for mapping network events](../../../reference-and-developer-docs/reference/xdm-fields-for-mapping-network-events).

| XDM Target Field              | Data Type | Purpose and Guidance                                                                                             |
| ----------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------- |
| `xdm.event.outcome`           | Enum      | **The vendor action.** Map `allow`/`permit` to `SUCCESS`; `deny`/`drop`/`block` to `FAILED`. Pad with `UNKNOWN`. |
| `xdm.event.tags`              | Array     | Must include `XDM_CONST.EVENT_TAG_NETWORK`.                                                                      |
| `xdm.event.type`              | String    | Must resolve to a value containing `network`. Pad as `"network"`.                                                |
| `xdm.network.ip_protocol`     | Enum      | Map using `XDM_CONST.IP_PROTOCOL_*`. Use `IP_PROTOCOL_IP` as the neutral default if the protocol is unknown.     |
| `xdm.network.protocol_layers` | Array     | `arraycreate(...)` over known layers (e.g., "HTTP", "IP"). Pure pad `arraycreate("IP")`.                         |
| `xdm.source.host.device_id`   | String    | Stable client device ID. Pad with `""`.                                                                          |
| `xdm.source.ipv4`             | String    | The observed client IPv4 address. Pad `""` only if the source is IPv6-only.                                      |
| `xdm.source.ipv6`             | String    | Map observed IPv6 address; pad `""` when the source is IPv4-only.                                                |
| `xdm.source.is_internal_ip`   | Boolean   | **Derive via rule.** Use `incidr()` over RFC 1918 ranges. Pure pad `false`.                                      |
| `xdm.source.port`             | Integer   | Client source port. Pad with `to_integer(0)`.                                                                    |
| `xdm.source.sent_bytes`       | Integer   | Total bytes sent by the source. Pad with `to_integer(0)`.                                                        |
| `xdm.target.host.device_id`   | String    | Stable target device ID. Pad with `""`.                                                                          |
| `xdm.target.ipv4`             | String    | The observed target IPV4 address. Pad `""` only if the target is IPv6-only.                                      |
| `xdm.target.ipv6`             | String    | Map observed IPv6 address; pad `""` when the target is IPv4-only.                                                |
| `xdm.target.is_internal_ip`   | Boolean   | **Derive via rule.** Use `incidr()` over RFC 1918 ranges. Pure pad `false`.                                      |
| `xdm.target.port`             | Integer   | Target destination port. Pad with `to_integer(0)`.                                                               |
| `xdm.target.sent_bytes`       | Integer   | Total bytes received by the source (sent by the target). Pad with `to_integer(0)`.                               |

</details>
