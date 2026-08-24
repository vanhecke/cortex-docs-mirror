---
description: Define COLLECT sections in Cortex XSIAM Parsing Rules.
---

# COLLECT

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

A `COLLECT` section defines a rule that enables data reduction and data manipulation at the Broker VM to help avoid sending unnecessary data to the Cortex XSIAM server and reduces traffic, storage, and computing costs. In addition, the `COLLECT` section is used to manipulate, alter, and enrich the data before it’s passed to the Cortex XSIAM server. While this rule is optional to configure, once added, this rule runs before the `INGEST` section.

{% hint style="info" %}
### Note

The [CSV Collector applet](../../../cortex-xsiam-data-sources/generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-csv-collector) is not affected by the `COLLECT` rules applied to a Broker VM.
{% endhint %}

To avoid performance issues on the Broker VM, Cortex XSIAM does not permit all Parsing Rules to run on the Broker VM by default, but only the Parsing Rules that you designate.

The Broker VM is directly affected by the `[COLLECT]` rules you create, so depending on the complexity of the rules more hardware resources on the Broker VM may be required. As a result, ensure that your Broker VM meets the following minimum hardware requirements to run `[COLLECT]` rules:

* 8-core processor
* 8GB RAM
* 512GB disk
* Plan for a max of 10K eps (events per second) per core.

`COLLECT` syntax is derived from Cortex Query Language (XQL) with a few modifications as explained in the [Parsing Rules file structure and syntax](). In addition, `COLLECT` rules contain the following syntax add-ons:

* `COLLECT` rules can have more than one XQLp statement, separated by a semicolon (`;`). Each statement creates a different data reduction and manipulation at the Broker VM for a different vendor and product.
* While the XQL stages [alter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/alter) and [fields](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/fields) are permitted in `COLLECT` rules for various vendors and products, you should avoid using them for supported vendors that can be used for Analytics as these stages can disrupt the operation of the Analytics Engine. For a list of these vendors, see the [Visibility of logs and alerts from external sources](https://app.gitbook.com/s/FOhYBYLdbwpnbJgr6uaX/cortex-xdr-3.x-documentation/data-management/data-ingestion/visibility-of-logs-and-alerts-from-external-sources) table specifically those vendors with Normalized Log Visibility.
* Another new stage is available called `drop`.
  * `drop` takes a condition similar to the XQL `filter` stage (same syntax), but drops every log entry that passes that condition. One can think of it as a negative filter, so `drop <condition>` is not equivalent to `filter not <condition>`.
  * `drop` can only appear last in a statement. No other XQLp syntax can follow.
*   `COLLECT` sections take parameters, where some are mandatory and others optional.

    ```programlisting
    [COLLECT:vendor=<vendor>, product=<product>, target_brokers = (<broker_ID1, brokerID2,...>), no_hit = <keep\drop>];
    ```

    Here's an example of how to define the `COLLECT` section with a single `broker_ID`:

    ```programlisting
    [COLLECT:vendor="PANW", product="NGFW_CEF", target_brokers=(BROKER_ID), no_hit=drop]
    ```

    Here's an example of how to define the `COLLECT` section with multiple `broker_ID`s:

    ```programlisting
    [COLLECT:vendor="PANW", product="NGFW_CEF", target_brokers=(BROKER_ID1, BROKER_ID2, BROKERID3), no_hit=drop]
    ```

The parameter descriptions are explained in the following table:

| Parameter        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vendor`         | The vendor that the specified `COLLECT` rule for data reduction and data manipulation at the Broker VM applies to (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `product`        | The product that the specified `COLLECT` rule for data reduction and data manipulation at the Broker VM applies to (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `target_brokers` | <p>Specifies the list of Brokers to run the <code>COLLECT</code> rule for data reduction and data manipulation based on the vendor and product configured (mandatory). When <code>target_brokers=*</code>, the <code>COLLECT</code> rule applies to all the data collected by the Broker VM applets.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The <a href="../../../cortex-xsiam-data-sources/generic-on-premise-data-collectors/broker-vm-data-collector-applets/activate-csv-collector">CSV Collector applet</a> is not affected by the <code>COLLECT</code> rules applied to a Broker VM.</p></div> |
| `no_hit`         | <p>No-match strategy to use for the entire specified group of <code>COLLECT</code> rules (optional). The default is <code>keep</code>.</p><ul><li>If <code>no_hit = drop</code>, then in a scenario where none of the <code>COLLECT</code> rules in the group generates output for a given event, that event is discarded.</li><li>If <code>no_hit = keep</code>, then in a scenario where none of the <code>COLLECT</code> rules in the group generates output for a given event, that event is passed to the Cortex XSIAM server.</li></ul>                                                                                                                                      |

The following is an example of using a `COLLECT` rule to filter data for a specific vendor and product that will run before the `INGEST` section.

```programlisting
[COLLECT:vendor="Apache", product="ApacheServer", target_brokers = (bvm1, bvm2, bvm3), no_hit = drop]
alter source_log = json_extract_scalar(_raw_log, "$.source") 
| filter source_log = "WebApp-Logs"
| fields source_log, _raw_log;
[INGEST:vendor="Apache", product="ApacheServer", target_dataset = "dvwa_application_log"]
alter log_timestamp = json_extract_scalar(_raw_log, "$.timestamp")
| alter log_msg = json_extract_scalar(_raw_log, "$.msg")
| alter log_remote_ip = json_extract_scalar(_raw_log, "$.Remote_IP")
| alter scanned_ip = json_extract_scalar(_raw_log, "$.Scanned_IP")
| fields log_msg ,log_remote_ip ,log_timestamp ,source_log ,scanned_ip , _raw_log;
```

A few more points to keep in mind when writing `COLLECT` rules:

*   There are no `COLLECT` rules by default, so all collected events are forwarded by the Broker VM to the Cortex XSIAM server.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>To reduce the amount of data transmitted to Cortex XSIAM from the broker, use filters to drop logs. Yet, be aware that once the logs are modified using <code>alter</code> or <code>fields</code> stages, the Broker VM will convert the original log into a JSON format, which could increase the data size being sent from the broker to Cortex XSIAM.</p></div>
* When `COLLECT` rules are defined, the designated Broker VMs check every collected event versus each rule. When there is a match for a given product or vendor, the Broker VM checks if it meets the filter criteria.
  * If it meets the criteria, the event is passed to the Cortex XSIAM server.
  *   If it doesn’t meet the criteria, it depends on the `no_hit` parameter.

      -If `no_hit=drop`, then this `COLLECT` rule will not pass the event. Yet, the event still goes through other rules on this Broker VM.

      -If `no_hit=keep`, the event is passed to the Cortex XSIAM server, and goes through other rules on this Broker VM.
* When the evaluated event, doesn’t match any product or vendor for a defined `COLLECT` rule, the event is passed to the Cortex XSIAM server.
