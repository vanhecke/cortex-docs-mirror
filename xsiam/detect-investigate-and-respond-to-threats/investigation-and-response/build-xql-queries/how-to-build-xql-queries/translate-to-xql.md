---
description: Translate searches and query logic into XQL with Cortex XSIAM .
---

# Translate to XQL

To help you easily convert your existing Splunk queries to the Cortex Query Language (XQL) syntax, Cortex XSIAM includes a toggle called **Translate to XQL** in the query ﬁeld in the user interface. When building your XQL query and this option is selected, both a **SPL query** field and **XQL query** field are displayed, so you can easily add a Splunk query, which is converted to XQL in the XQL query field. This option is disabled by default, so only the **XQL query** field is displayed.

{% hint style="info" %}
### Important

This feature is still in a Beta state and you will find that not all Splunk queries can be converted to XQL. This feature will be improved upon in the upcoming releases to support greater Splunk query translations to XQL.
{% endhint %}

<details>

<summary>Supported functions in Splunk</summary>

The following table details the supported functions in Splunk that can be converted to XQL in Cortex XSIAM with an example of a Splunk query and the resulting XQL query. In each of these examples, the `xdr_data` dataset is used.

| Splunk Function/Stage       | Splunk Query Example                                                                                                               | Resulting XQL Query Example                                                                                     |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `avg`                       | \`index=xdr\_data                                                                                                                  | stats avg(dst\_association\_strength)\`                                                                         |
| `bin`                       | \`index = xdr\_data                                                                                                                | bin \_time span=5m\`                                                                                            |
| `coalesce`                  | \`index= xdr\_data                                                                                                                 | eval product\_or\_vendor\_not\_null=coalesce(\_product, \_vendor )\`                                            |
| `count`                     | \`index=xdr\_data                                                                                                                  | stats count(\_product) BY \_time\`                                                                              |
| `ctime`                     | \`index=xdr\_data                                                                                                                  | convert ctime(field) as field\`                                                                                 |
| `earliest`                  | `index = xdr_data earliest=24d`                                                                                                    | \`dataset in (xdr\_data)                                                                                        |
| `eval`                      | \`index=xdr\_data                                                                                                                  | eval field = "test"\`                                                                                           |
| `fillnull`                  | \`index=xdr\_data                                                                                                                  | fillnull value = "missing ipv6" agent\_ip\_addresses\_v6\`                                                      |
| `floor`                     | \`index=xdr\_data                                                                                                                  | eval floor\_test = floor(1.9)\`                                                                                 |
| `iplocation`                | \`index=xdr\_data                                                                                                                  | inputlookup append=true my\_lookup.csv\`                                                                        |
| `iplocation`                | \`index = xdr\_data                                                                                                                | inputlookup agent\_ip\_addresses\`                                                                              |
| `isnotnull`                 | \`index=xdr\_data                                                                                                                  | eval x = isnotnull(agent\_hostname)\`                                                                           |
| `isnull`                    | \`index=xdr\_data                                                                                                                  | eval x = isnull(agent\_hostname)\`                                                                              |
| `json_extract`              | \`index= xdr\_data                                                                                                                 | eval London=json\_extract(dfe\_labels,"dfe\_labels{0}")\`                                                       |
| `join`                      | `join agent_hostname [index = xdr_data]`                                                                                           | `join type=left conflict_strategy=right (dataset in (xdr_data)) as inner agent_hostname = inner.agent_hostname` |
| `latest`                    | `index = xdr_data latest=-24d`                                                                                                     | \`dataset in (xdr\_data)                                                                                        |
| `len`                       | \`index = xdr\_data                                                                                                                | where uri != null                                                                                               |
| `ltrim(<str>,<trim_chars>)` | \`index=xdr\_data                                                                                                                  | eval trimed\_agent=ltrim("agent\_hostname", "agent\_")\`                                                        |
| `lower`                     | \`index = xdr\_data                                                                                                                | eval field = lower("TEST")\`                                                                                    |
| `max`                       | \`index =xdr\_data                                                                                                                 | stats max(action\_file\_size) by \_product\`                                                                    |
| `md5`                       | \`index=xdr\_data                                                                                                                  | eval md5\_test = md5("test")\`                                                                                  |
| `median`                    | \`index = xdr\_data                                                                                                                | stats median(actor\_process\_file\_size) by \_time\`                                                            |
| `min`                       | \`index =xdr\_data                                                                                                                 | stats min(action\_file\_size) by \_product\`                                                                    |
| `mvcount`                   | \`index = xdr\_data                                                                                                                | where http\_data != null                                                                                        |
| `mvdedup`                   | \`index = xdr\_data                                                                                                                | eval s=mvdedup(action\_app\_id\_transitions)\`                                                                  |
| `mvexpand`                  | \`index = xdr\_data                                                                                                                | mvexpand dfe\_labels limit = 100\`                                                                              |
| `mvfilter`                  | \`index = xdr\_data                                                                                                                | eval x = mvfilter(isnull(dfe\_labels))\`                                                                        |
| `mvindex`                   | \`index=xdr\_data                                                                                                                  | eval field = mvindex(action\_app\_id\_transitions, 0)\`                                                         |
| `mvjoin`                    | \`index=xdr\_data                                                                                                                  | eval n=mvjoin(action\_app\_id\_transitions, ";")\`                                                              |
| `pow`                       | \`index=xdr\_data                                                                                                                  | eval pow\_test = pow(2, 3)\`                                                                                    |
| `relative_time(X,Y)`        | <ul><li>`index ="xdr_data"</li></ul>                                                                                               | where \_time > relative\_time(now(),"-7d@d")`</li><li>`index ="xdr\_data"                                       |
| `replace`                   | \`index= xdr\_data                                                                                                                 | eval description = replace(agent\_hostname,"("."NEW")\`                                                         |
| `rex`                       | \`index=xdr\_data action\_local\_ip!="0.0.0.0"                                                                                     | rex field=action\_local\_ip "(?\<src\_ip>\d+.\d+.\d+.48)"                                                       |
| `round`                     | \`index=xdr\_data                                                                                                                  | eval round\_num = round(3.5)\`                                                                                  |
| `rtrim`                     | \`index=xdr\_data                                                                                                                  | eval trimed\_hostname=rtrim("agent\_hostname", "hostname")\`                                                    |
| `search`                    | \`index = xdr\_data                                                                                                                | eval ip="192.0.2.56"                                                                                            |
| `sha256`                    | \`index = xdr\_data                                                                                                                | eval sha256\_test = sha256("test")\`                                                                            |
| `sort (ascending order)`    | \`index = xdr\_data                                                                                                                | sort action\_file\_size\`                                                                                       |
| `sort (descending order)`   | \`index = xdr\_data                                                                                                                | sort -action\_file\_size\`                                                                                      |
| `spath`                     | \`index = xdr\_data                                                                                                                | spath output=myfield input=action\_network\_http path=headers.User-Agent\`                                      |
| `split`                     | \`index = xdr\_data                                                                                                                | where mac != null                                                                                               |
| `stats`                     | \`index=xdr\_data                                                                                                                  | stats count(event\_type) by \_time\`                                                                            |
| `stats dc`                  | \`index = xdr\_data                                                                                                                | stats dc(\_product) BY \_time\`                                                                                 |
| `strcat`                    | \`index=xdr\_data                                                                                                                  | strcat story\_id "/" http\_req\_before\_method comboIP\`                                                        |
| `sum`                       | \`index=xdr\_data                                                                                                                  | where action\_file\_size != null                                                                                |
| `table`                     | \`index = xdr\_data                                                                                                                | table \_time, agent\_hostname, agent\_ip\_addresses, \_product\`                                                |
| `tonumber`                  | \`index=xdr\_data                                                                                                                  | eval tonumber\_test = tonumber("90210")\`                                                                       |
| `top`                       | <p>The following Splunk functions can be translated to XQL:</p><ul><li><p><code>limit</code></p><p>`index = xdr_data</p></li></ul> | where action\_app\_id\_risk > 0                                                                                 |
| `upper`                     | \`index=xdr\_data                                                                                                                  | eval field = upper("test")\`                                                                                    |
| `var`                       | \`index=xdr\_data                                                                                                                  | stats var (event\_type) by \_time\`                                                                             |

</details>

<details>

<summary>How to translate a Splunk query to XQL syntax</summary>

1. Select **Investigation & Response** → **Search** → **Query Builder** → **XQL**.
2. Toggle to **Translate to XQL**, where both a **SPL query** field and **XQL query** field are displayed.
3. Add your Splunk query to the **SPL query** field.
4.  Click the arrow (<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-71323bbde54be11af6b419e0c345f2d01f50d2f5%2F49c8fc73157209b7a766a070aef61257efb9b7d6ddc22957f2c8ae2c8e9084a2.png?alt=media" alt="translate-to-spl-arrow.png" data-size="line">).

    The **XQL query** field displays the equivalent Splunk query using the XQL syntax.

    You can now decide what to do with this query based on the instructions explained in [Create XQL query](create-xql-query).

</details>
