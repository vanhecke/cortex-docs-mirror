# Create a query from a template

You can use the Query Builder templates to create effective queries without using the Cortex Query Language (XQL).

Review the following topics:

* [Query Builder templates]()
* [Get started with Query Builder templates](get-started-with-query-builder-templates)
* [Considerations for using Query Builder templates](considerations-for-using-query-builder-templates)

### How to create a query from a Query Builder template

1. Select **Investigation & Response** → **Search** → **Query Builder**.
2.  In the Query Builder, select the template that you want to use.

    If you want to use the Free Text Search template, see [Run a free text query](run-a-free-text-query).
3. (Optional) Change the **Run on** option (upper-right corner) that controls the datasets configured to run with the template. The templates are automatically configured to run on default datasets or you can choose to run them on all datasets. The templates run on the following datasets by default:
   * **Basic**, **Identity**, **Endpoint**, and **Network** templates: `xdr_data`
   * **Cloud** template: `cloud_audit_logs`
4. Enter values for any of the predefined fields and specify whether to include **Empty values** in the query.

<details>

<summary>Guidelines</summary>

* The query uses an AND operator between the filtering fields.
* Separate multiple values with pipes and do not add spaces between the value and the pipe.
* Some of the filtering fields are aliases and therefore search all fields that are associated with the alias.
* You can run an empty template with no values specified. The query results will show data from all of the fields in the template specific fieldset.

For more information about using the filtering fields, operators, and including **Empty values**, see [Considerations for using Query Builder templates](considerations-for-using-query-builder-templates).

</details>

5\. (Optional) Click **Add Field** and select the additional filtering fields or aliases to include in the query."

{% hint style="info" %}
### Note

* Field names and aliases are listed without their prefix, for example **xdm.SOURCE.USER.USERNAME** is listed as **SOURCE.USER.USERNAME** and **XDM\_ALIAS.ipv4** is listed as **ipv4**.
* Fields that are already included in the query template are shown as grayed out.
* In the Identity and Network templates, `xdm.event.outcome` shows as grayed out. In these templates, the **ACTION STATUS** and **CONNECTION STATUS** fields are linked to the `xdm.event.outcome` enum. Therefore, you can't duplicate this field in a query.
{% endhint %}

6\. Click **TIME** and select a time frame for the query.

7.  Click **Run** to start the query, or click **Schedule** to run the query at a specific time.

    You can also click **Continue in XQL** to open the XQL Query Builder showing the defined XQL fields. In XQL you have the flexibility to add additional stages and functions that are not available in the Query Builder templates.
8.  Review the **Results**.

    The search is limited to 1,000 results. In the **Fields** column, you can see all of the fields that were included in the query in the following order: (1) **\_time**, (2) the filtering fields that you defined, and (3) the fields from the template-specific fieldset.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>This order might change if you include a filtering field that is listed in the fieldset. In that case, the field is taken out of the fieldset and ordered at the top of the list with the other filtering fields.</p></div>

    The query is also saved in the Query Center. In the Query Center, you can identify your query by filtering the **Created By** column and looking in the **Query Description** column. Queries created from a template are prefixed with the template name.

#### **Example**

*   The following query searches for instances of IP 3.3.3.3 with a source host name equal to host1 or host2. IP is an alias field; therefore, the query searches all fields associated with the alias.

    ```programlisting
    IP ADDRESS = 3.3.3.3, SOURCE.HOST.OS = host1|host2
    ```
*   The following query searches for the event outcome success with an event duration value that is not equal to null:

    ```programlisting
    EVENT.OUTCOME = XDM_CONST.OUTCOME_SUCCESS, EVENT.DURATION != Empty values
    ```

#### **What to do next**

* To edit or rerun the query, click **Back to edit** to review the template, or **Continue in XQL** to review the XQL.
* Practice running queries with [Query Builder template examples](query-builder-template-examples).
