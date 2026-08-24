---
description: Learn Cortex XSIAM Parsing Rules file structure and XQLp syntax.
---

# Parsing Rules file structure and syntax

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

<details>

<summary>File structure</summary>

The Parsing Rules file consists of multiple sections of these three types, which also represent the custom syntax specific to Parsing Rules.

* `INGEST`: This section is used to define the resulting dataset.
* `COLLECT` (Optional): This section defines a rule that enables data reduction and data manipulation at the Broker VM to help avoid sending unnecessary data to the Cortex XSIAM server and reduce traffic, storage, and computing costs. In addition, the `COLLECT` section is used to manipulate, alter, and enrich the data before it’s passed to the Cortex XSIAM server. While this rule is optional to configure, once added this rule runs before the `INGEST` section.
* `CONST` (Optional): This section is used to define strings and numbers that can be reused multiple times within Cortex Query Language (XQL) statements in other `INGEST` sections by using `$constName`.
* `RULE` (Optional): Rules are part of the XQL syntax, which are tagged with a name, and can be reused in the code in the `INGEST` sections by using `[rule:ruleName]`.
* `EXTEND` (Optional): This section is used to chain your Parsing Rules logic to extend your existing default `RULE` sections, which are added by a Content Package you installed from the Marketplace. An `EXTEND` section runs immediately after the default `RULE` section that it extends and enables data manipulation without overriding or interfering with the existing vendor Parsing Rules.

The order of the sections is unimportant. The data of each section type gets grouped together during the parsing stage. Before any action takes place all `COLLECT`, `CONST`, `RULE`, `EXTEND`, and `INGEST` objects are grouped together and collected to the same list.

</details>

<details>

<summary>Syntax</summary>

The syntax used in the Parsing Rules file is derived from XQL, but with a few modifications. This subset of XQL is called XQL for Parsing (XQLp).

{% hint style="info" %}
### Note

For more information on the XQL syntax, see Cortex XQL Language Reference.
{% endhint %}

The `COLLECT`, `CONST`, `INGEST`, `RULE`, and `EXTEND`syntax is derived from XQL, but with the following modifications for XQLp:

* A statement never starts with a dataset or preset selection. The query's data source is meaningless. It is transparent to the user where the raw logs are coming from, fully handled by the system.
*   Only the following XQL stages are permitted: [alter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/alter), [fields](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/fields), [filter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/filter), and [join](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/join). In addition, a new `call` stage is supported, which is used to invoke another rule.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><ul><li>An <code>inner</code> type of <code>join</code> stage is only supported in <code>CONST</code>, <code>INGEST</code>, and <code>RULE</code> sections and is not supported in a <code>COLLECT</code> section.</li><li>You cannot <code>call</code> a <code>RULE</code> section that exists in <strong>Default Rules</strong> from the <strong>User Defined Rules</strong> section.</li></ul></div>
*   Only the following XQL functions are permitted in all sections: [parse\_timestamp](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/parse_timestamp), [parse\_epoch](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/parse_epoch), and [regexcapture](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/regexcapture).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The <a href="https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/functions/regexcapture">regexcapture</a> function is only supported in Parsing Rules and cannot be used in any other XQL query.</p></div>
* No output stages are supported.
* A `Rule` object can only contain a single statement.
*   A `join inner` query is restricted to using a lookup as a data source and is only supported in XQLp stages.

    There is no default lookup, so all `join inner` queries must start with `dataset=<lookup> | ...`.
* `CONST` reference (`$MY_CONST`) is supported.
* An `IN` condition can only take a sequence list, such as `device_name in (“device1”, “device2”, “device3”)` and not another XQL or XQLp `inner` queries.
* You can't create parsing rules for Next-Generation Firewall (NGFW) datasets that are in the format `panw_ngfw_<text>_raw`, and the Observability dataset called `panw_observability_raw`.

Comments in C programming language can be used anywhere throughout the Parsing Rules file:

```programlisting
// line comment
/* inner comment */
```

{% hint style="info" %}
### Note

Every statement in the Parsing Rules file must end with a semicolon (`;`).
{% endhint %}

</details>
