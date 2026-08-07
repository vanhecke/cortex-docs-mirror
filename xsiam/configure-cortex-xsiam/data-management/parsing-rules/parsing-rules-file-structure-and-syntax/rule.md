# RULE

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

Rules are very similar to functions in modern programming languages. They are essentially pieces of Cortex Query Language (XQL) syntax, tagged with a name - alias, for easier code reuse and avoiding code duplications. A `RULE` is an add-on to the Parsing Rule syntax and is optional to configure.

`RULE` syntax is derived from XQL with a few modifications, as explained in the [Parsing Rules file structure and syntax]().

{% hint style="info" %}
### Note

For more information on the XQL syntax, see [Get started with XQL](../../../../reference-and-developer-docs/cortex-agentix-xql/get-started-with-xql).
{% endhint %}

A few more points to keep in mind when writing `RULE` sections.

*   Rules are defined by `[rule:ruleName]` as depicted in the following example:

    ```programlisting
    [rule:filter_issues]
    filter raw_log not contains "issue";
    ```
*   Rules are invoked by using a `call` keyword as depicted in the following example:

    ```programlisting
    [rule:filter_issues]
    filter raw_log not contains "issue"; 
    [rule:use_another_rule]
    filter severity="LOW" | call filter_issues | fields - raw_log;
    ```

    This is equivalent to writing:

    ```programlisting
    [rule:use_another_rule]
    filter severity="LOW" | filter raw_log not contains "issue" | fields - raw_log;
    ```
* Rule names are not case-sensitive. They can be written in any user-desired casing, such as UPPER\_SNAKE, lower\_snake, camelCase, and CamelCase). For example, `MY_RULE=My_Rule=my_rule`.
* Rule names must be unique across the entire file. This means you cannot have the same rule name defined more than once in the same file.
* Since section order is unimportant, you do not have to declare a `rule` before using it. You can have the `rule` definition section written below other sections that use this rule.
*   You can add a single tag or list of tags to the ingested data as part of the ingestion flow that you can easily query. You can add tags using both the `INGEST` and `RULE` sections.

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
    tag add "test1", "test2", "test3";
    ```

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can also add tags using only the <code>INGEST</code> section. For more information, see <a href="ingest">INGEST</a>.</p></div>
