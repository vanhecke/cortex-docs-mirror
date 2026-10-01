---
description: >-
  Map network events to Cortex XSIAM XDM fields for normalized identity data and
  authentication stories.
---

# XDM fields for mapping network events

This section provides a comprehensive guide to mapping network traffic events from various customer log sources to the Cortex Data Model (XDM) schema. Each relevant XDM field is detailed, including whether the field is mandatory or optional, the corresponding network story field, data type, and purpose, ensuring consistent data normalization essential for robust security analysis and threat detection.

The fields that are mandatory to map are listed below with an asterisk (\*) beside them as these fields must be mapped to automatically create network stories for XDM data.

Once these network events are mapped, Cortex XSIAM provides out-of-the-box detection logic for third-party firewalls. For more information, see [Third-Party Firewalls](https://cortex-docs.paloaltonetworks.com/analytics-alerts/alerts-by-data-source/third-party-firewalls).

{% hint style="info" %}
### Note

* For more information on the entire Cortex Data model (XDM) schema, see [Cortex XSIAM Data Model Schema](https://cortex-docs.paloaltonetworks.com/xsiam-data-model-schema).
* For technical conventions and implementation logic for complex authentication scenarios, see [Advanced network mapping: deep dives](xdm-fields-for-mapping-network-events/advanced-network-mapping-deep-dives).
{% endhint %}

### Mandatory XDM fields for network events

#### 1. xdm.event.outcome\*

* **Network Story Field**: `action_outcome`
* **Type**: enum
* **Requirement**: Mandatory
* **Description**: The final result of the network connection attempt.
* **Supported values**: Map vendor actions like allow/permit to `XDM_CONST.OUTCOME_SUCCESS` and deny/drop/block to `XDM_CONST.OUTCOME_FAILED`. Pad with `XDM_CONST.OUTCOME_UNKNOWN`.

#### 2. xdm.event.tags\*

* **Network Story Field**: `dfe_labels`
* **Type**: array
* **Requirement**: Mandatory
* **Description**: Tags applied to the event for story stitching.
* **Supported values**: Must include `XDM_CONST.EVENT_TAG_NETWORK`.

#### 3. xdm.event.type\*

* **Network Story Field**: `event_type`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: The primary event classification.
* **Note**: Must resolve to a value that contains `network`. Pad with the literal `"network"`.

#### 4. xdm.network.ip\_protocol\*

* **Network Story Field**: `action_network_protocol`
* **Type**: integer (enum)
* **Requirement**: Mandatory
* **Description**: The transport protocol used for the connection.
* **Supported values**: Map using `XDM_CONST.IP_PROTOCOL_*` (e.g., `IP_PROTOCOL_TCP`). Use `IP_PROTOCOL_IP` as the neutral default if unknown.

#### 5. xdm.network.protocol\_layers\*

* **Network Story Field**: `action_app_id_transitions`
* **Type**: array
* **Requirement**: Mandatory
* **Description**: The stack of protocol layers identified in the traffic.
* **Implementation**: `arraycreate(...)` over known layers (e.g., "HTTP", "IP"). Pure pad `arraycreate("IP")`.

#### 6. xdm.source.host.device\_id\*

* **Network Story Field**: `agent_id`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: Stable identifier for the client device.
* **Note**: Pad with an empty string `""` if unavailable.

#### 7. xdm.source.ipv4\*

* **Network Story Field**: `action_local_ip`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: The observed IPv4 address of the client/source.
* **Note**: Pad with `""` only if the source is IPv6-only.

#### 8. xdm.source.ipv6\*

* **Network Story Field**: `action_local_ip`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: The observed IPv6 address of the client/source.
* **Note**: Pad with `""` if the source is IPv4-only.

#### 9. xdm.source.is\_internal\_ip\*

* **Network Story Field**: `is_internal_ip`
* **Type**: boolean
* **Requirement**: Mandatory
* **Description**: Indicates if the source IP is internal to the network.
* **Implementation**: Derive using `incidr()` over RFC 1918 ranges. Pure pad `false`.

#### 10. xdm.source.port\*

* **Network Story Field**: `action_local_port`
* **Type**: integer
* **Requirement**: Mandatory
* **Description**: The source port of the client connection.
* **Implementation**: Map the real value; otherwise `to_integer(0)`.

#### 11. xdm.source.sent\_bytes\*

* **Network Story Field**: `action_total_upload`
* **Type**: integer
* **Requirement**: Mandatory
* **Description**: Total bytes sent by the source side.
* **Implementation**: Map the real value; otherwise `to_integer(0)`.

#### 12. xdm.target.host.device\_id\*

* **Network Story Field**: `dst_agent_id`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: Stable identifier for the target device.
* **Note**: Pad with an empty string `""` if unavailable.

#### 13. xdm.target.ipv4\*

* **Network Story Field**: `action_remote_ip`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: The observed IPv4 address of the target/destination.
* **Note**: Pad with `""` only if the target is IPv6-only.

#### 14. xdm.target.ipv6\*

* **Network Story Field**: `action_remote_ip`
* **Type**: string
* **Requirement**: Mandatory
* **Description**: The observed IPv6 address of the target/destination.
* **Note**: Pad with `""` if the target is IPv4-only.

#### 15. xdm.target.is\_internal\_ip\*

* **Network Story Field**: `dst_is_internal_ip`
* **Type**: boolean
* **Requirement**: Mandatory
* **Description**: Indicates if the target IP is internal to the network.
* **Implementation**: Derive using `incidr()` as for the source; pure pad `false`.

#### 16. xdm.target.port\*

* **Network Story Field**: `action_remote_port`
* **Type**: integer
* **Requirement**: Mandatory
* **Description**: The destination port of the connection.
* **Implementation**: Map the real value; otherwise `to_integer(0)`.

#### 17. xdm.target.sent\_bytes\*

* **Network Story Field**: `action_total_download`
* **Type**: integer
* **Requirement**: Mandatory
* **Description**: Total bytes sent by the target (received by the source).
* **Implementation**: Map the real value; otherwise `to_integer(0)`.

### HTTP set mandatory XDM fields

These two fields are mandatory only if your network event carries an HTTP layer (such as Proxy or WAF) and they are configured together.

#### 18. xdm.network.http.http\_header.header\*

* **Network Story Field**: The following header values are supported, which are then mapped to the `xdm.network.http.http_header.value` network story field (see below):
  * `Content-Length`
  * `User-Agent`
  * `Host`
  * `Content-Type`
  * `Referer`
* **Type**: string
* **Requirement**: Mandatory (for HTTP events)
* **Description**: The HTTP header name. Map when logs carry headers; otherwise `""`. The bare `xdm.network.http.http_header` is a container node, not a mappable field, so some data models reject it.

#### 19. xdm.network.http.http\_header.value\*

* **Network Story Field**: The following fields are supported based on the `xdm.network.http.http_header.header` network story field values as listed above:
  * **Content-Length**: `http_data.http_req_content_length`
  * **User-Agent**: `http_data.http_req_user_agent_header`
  * **Host**: `http_data.http_req_host_header`
  * **Content-Type**: `http_data.http_req_content_type_header`
  * **Referer**: `http_data.http_req_referer_header`
* **Type**: string
* **Requirement**: Mandatory (for HTTP events)
* **Description**: The HTTP header value. Map when logs carry headers; otherwise `""`. The bare `xdm.network.http.http_header` is a container node, not a mappable field, so some data models reject it.

### Optional XDM fields for network events

#### 20. xdm.network.http.url\_category

* **Network Story Field**: `dst_action_url_category`
* **Type**: enum
* **Requirement**: Optional
* **Description**: The vendor-assigned URL category.
* **Implementation**: Map to the closest `XDM_CONST.URL_CATEGORY_*` member; pad `URL_CATEGORY_UNKNOWN`.

#### 21. xdm.network.dns.dns\_question.name

* **Network Story Field**: `dns_query_name`
* **Type**: string
* **Requirement**: Optional
* **Description**: The queried domain name for DNS traffic.

#### 22. xdm.network.http.url

* **Network Story Field**: `http_data.http_req_uri_path`
* **Type**: string
* **Requirement**: Optional
* **Description**: The full requested URL.

#### 23. xdm.network.tls

* **Network Story Field**: `ssl_data`
* **Type**: string
* **Requirement**: Optional
* **Description**: TLS summary string.

#### 24. xdm.source.user.username

* **Network Story Field**: `actor_primary_username`
* **Type**: string
* **Requirement**: Optional
* **Description**: Human-readable display name for the source user.

#### 25. xdm.target.file.filename

* **Network Story Field**: `file_data.file_name`
* **Type**: string
* **Requirement**: Optional
* **Description**: Name of the file being transferred.

#### 26. xdm.target.host.hostname

* **Network Story Field**: `dst_agent_hostname`
* **Type**: string
* **Requirement**: Optional
* **Description**: Hostname of the target device.
