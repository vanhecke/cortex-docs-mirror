# INGEST

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

An `INGEST` section is used to define the resulting dataset. The `COLLECT`, `CONST`, and `RULE` sections are only add-ons, used to help organize the `INGEST` sections, and are optional to configure. Yet, a Parsing Rules file that contains no `INGEST` sections, generates no Parsing Rules. Therefore, the `INGEST` section is mandatory to configure.

`INGEST` syntax is derived from Cortex Query Language (XQL) with a few modifications as explained in the [Parsing Rules file structure and syntax](). In addition, `INGEST` sections contain the following syntax add-ons:

* `INGEST` sections can have more than one XQLp statement, separated by a semicolon (`;`). Each statement creates a different Parsing Rule.
* The following XQL functions and stages are also supported in the `INGEST` section:
  * Functions: [arrayfilter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/arrayfilter), [arraycreate](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/arraycreate), [arraymerge](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/arraymerge), [object\_create](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/object_create), [parse\_cef,](ingest/parse_cef) [parse\_cisco](ingest/parse_cisco), and [parse\_json](ingest/parse_json).
  * Stages: [iploc](https://app.gitbook.com/s/FOhYBYLdbwpnbJgr6uaX/cortex-xdr-3.x-documentation/cortex-xdr-xql/stages/iploc) and [arrayexpand](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/arrayexpand).
    * [fields](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/fields): Using the `fields` stage in the `[INGEST]` section of the parsing rule explicitly controls the schema creation of the raw dataset. If you explicitly define only to ingest a few fields, then only these fields will be stored in Cortex XSIAM and available to query. Defining `fields` is a good way to only ingest clean data without including any corrupt data.
* Another new stage is available called `drop`.
  * `drop` takes a condition similar to the XQL `filter` stage (same syntax), but drops every log entry that passes that condition. One can think of it as a negative filter, so `drop <condition>` is not equivalent to `filter not <condition>`.
  * `drop` can only appear last in a statement. No other XQLp rules can follow.
*   `INGEST` sections take parameters, and not names as `RULE` sections use, where some are mandatory and others optional.

    ```programlisting
    [ingest:vendor=<vendor>, product=<product>, target_dataset=<dataset>, no_hit=<keep\drop>, ingestnull=<true\false>]
    filter raw_log not contains "issue";
    ```

The parameter descriptions are explained in the following table:

| Parameter        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vendor`         | The vendor that the specified Parsing Rules apply to (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `product`        | The product that the specified Parsing Rules apply to (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `target_dataset` | The name of the dataset to insert every row with the results after applying any of the specified Parsing Rules (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `no_hit`         | <p>No-match strategy to use for the entire specified group of rules (optional). The default is <code>keep</code>.</p><ul><li>If <code>no_hit = drop</code>, then in a scenario where none of the rules in the group generates output for a given log record, that record is discarded.</li><li>If <code>no_hit = keep</code>, then in a scenario where none of the rules in the group generates output for a given log record, that record is kept in the <code>_raw_log</code> field. This record is inserted into the group's dataset once, but every column holds <code>NULL</code> except for <code>_raw_log</code>, which holds the original JSON log record.</li></ul> |
| `ingestnull`     | Defines whether null value fields are ingested (optional). By default this is set to `true`, so you only need to set this parameter when you want to overwrite the default definition.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

Each statement represents a different Parsing Rule in the same group as depicted in the following example:

```programlisting
[CONST]
DEVICE_NAME = "ngfw"; 
[rule:use_two_rules]
filter severity = "medium" | call basic_rule | call use_xql_and_another_rule; 
[rule:basic_rule]
fields log_type, severity | filter log_type="eal" and severity="HIGH" and type="something"; 
[rule:use_xql_and_another_rule]call multiline_statement | filter severity = "medium"; 
[rule:multiline_statement]
alter url = json_extract(_raw_log, "$.url")
| join type = inner conflict_strategy = both (dataset=my_lookup) as inn url=inn.url 
|filter severity = "medium"; 
[ingest:vendor=panw, product=ngfw, target_dataset=panw_ngfw_ds, no_hit=drop]
filter log_type="traffic" | alter url = json_extract(_raw_log, "$.url");
call use_two_rules | join type = inner conflict_strategy = both (dataset=my_lookup) as inn severity=inn.severity | fields severity, log_type | drop device_name = $DEVICE_NAME;
```

This generates 1 group of 2 Parsing Rules for panw/ngfw, where all the ingested data into `panw_ngfw_ds` dataset.

The following represents the syntax for the rules:

```programlisting
Rule #1:
filter log_type="traffic" | alter url = json_extract(_raw_log, "$.url"); 
Rule #2:
filter severity = "medium"
| fields log_type, severity
| filter log_type="eal" and severity="HIGH" and type="something"
| alter url = json_extract(_raw_log, "$.url")
| join type = inner conflict_strategy = both (dataset=my_lookup) as inn url=inn.url
| filter severity = "medium"
| filter severity = "medium"
| join type = inner conflict_strategy = both (dataset=my_lookup) as inn severity=inn.severity
| fields severity, log_type
| drop device_name = $DEVICE_NAME
```

A few more points to keep in mind when writing `INGEST` sections:

* `INGEST` parameter names are not case-sensitive. Therefore, `vendor=PANW` and `vendor=panw` are the same.
* Since section order is unimportant, you do not have to declare a `RULE` or a `CONST` before using it in an `INGEST` section.
*   You can have multiple `INGEST` sections with the same `vendor`, `product`, `dataset` , and `no_hit` values. Yet, this can lead to unexpected results. Consider the following example:

    Example 36.

    ```programlisting
    [ingest:vendor=panw, product=ngfw, tartget_dataset=panw_ngfw_ds, no_hit=keep]
    filter raw_log not contains "issue"; 
    [ingest:vendor=panw, product=ngfw, target_dataset=panw_ngfw_ds, no_hit=keep]
    filter device_type not contains "agent";
    ```

    Let `lw` be a log row. If `lw.raw_log` doesn't contain an `issue` and `lw.device_type` doesn't contain an `agent`, then `lw` is inserted twice into the `pan_ngfw_ds` dataset as every section is standalone.

    * To eliminate these kinds of errors and misunderstandings, it is highly advised to group all rules having the same `vendor`, `product`, `dataset` , and `no_hit` values in a single `INGEST` section.
    * Logs that were discarded by a `drop` stage are considered ingested with a no-match policy. This means they are not kept even if `no_hit = keep`.
    * Keep in mind that all rules inside a group get evaluated independently. This is in contrast to firewall-like rules, which stop evaluating the first rule that is able to make a decision. Therefore, without proper filtering, it is possible to ingest the same log more than once.
* You can override the default raw dataset in `INGEST` sections. For more information, see [Parsing Rules Raw Dataset](../parsing-rules-raw-dataset).
*   Cortex XSIAM supports configuring case sensitivity in Parsing Rules only within the `INGEST` section using the following configuration stage:

    ```programlisting
    config case_sensitive = true | false
    ```
*   You can add a single tag or list of tags to the ingested data as part of the ingestion flow that you can easily query. You can add tags as part of the `INGEST` section or use both the `INGEST` and `RULE` sections.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can't add tags to parsing rules using the Next-Generation Firewall (NGFW) datasets that are in the format <code>panw_ngfw_&#x3C;text>_raw</code>, and the Observability dataset called <code>panw_observability_raw</code>.</p></div>

    The following are examples of each:

    *   `INGEST` section:

        Adding a single tag:

        ```programlisting
        [INGEST:vendor="MSFT", product="Azure AD Audit", target_dataset="msft_ad_audit_tagging", no_hit=drop, ingestnull = false ]
        tag add "New Event"
        ```

        Adding a list of tags:

        ```programlisting
        [INGEST:vendor="MSFT", product="Azure AD Audit", target_dataset="msft_ad_audit_tagging", no_hit=drop, ingestnull = false ]
        tag add "New Event1", "New Event2", "New Event3"
        ```
    *   `INGEST` and `RULE` sections:

        Example 38.

        Adding a single tag:

        ```programlisting
        [INGEST:vendor="Check Point", product="Anti Malware", target_dataset="malware_test", no_hit= drop  , ingestnull = true ]
        alter xx = call new_tag_rule; 
        ```

        ```programlisting
        [RULE:new_tag_rule]
        tag add "test";
        ```

        Adding a list of tags:

        ```programlisting
        [INGEST:vendor="Check Point", product="Anti Malware", target_dataset="malware_test", no_hit= drop  , ingestnull = true ]
        alter xx = call new_tag_rule; 
        ```

        ```programlisting
        [RULE:new_tag_rule]
        tag add  "test1", "test2", "test3";
        ```
