---
description: Use the Cortex XSIAM Legacy Query Builder to query security data entities.
---

# Legacy Query Builder

{% hint style="info" %}
We recommend using the Query Builder in **New mode** to take advantage of the Query Builder templates and the ability to search the full Cortex Data Model (XDM).

In **Legacy mode**, the Query Builder searches predefined datasets only. To search the full XDM, switch to New mode or select XQL Search.
{% endhint %}

The **Legacy Query Builder** provides queries for the following types of entities:

* **Process**: Search on process execution and injection by process name, hash, path, command line arguments, and more. See [Create process query](legacy-query-builder/create-process-query).
* **File**: Search on file creation and modification activity by file name and path. See [Create file query](legacy-query-builder/create-file-query).
* **Network**: Search network activity by IP address, port, host name, protocol, and more. See [Create network query](legacy-query-builder/create-network-query).
* **Image Load**: Search on module load into process events by module IDs and more. See [Create image load query](legacy-query-builder/create-image-load-query).
* **Registry**: Search on registry creation and modification activity by key, key value, path, and data. See [Create registry query](legacy-query-builder/create-registry-query).
* **Event Log**: Search Windows event logs and Linux system authentication logs by username, log event ID (Windows only), log level, and message. See [Create event log query](legacy-query-builder/create-event-log-query).
* **Network Connections**: Search security event logs by firewall logs, endpoint raw data over your network. See [Create network connections query](legacy-query-builder/create-network-connections-query).
* **Authentications**: Search on authentication events by identity, target outcome, and more. See [Create authentication query](legacy-query-builder/create-authentication-query).
* **All Actions**: Search across all network, registry, file, and process activity by endpoint or process. See [Query across all entities](legacy-query-builder/query-across-all-entities).

The **Query Builder** also provides flexibility for both on-demand query generation and scheduled queries.
