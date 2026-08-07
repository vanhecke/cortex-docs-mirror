# Fetch issues from an integration instance

You can poll third-party integration instances for events and turn them into Cortex XSIAM issues (fetching). Many integrations support fetching, but not all support this feature. You can view each integration in the [Developer Hub](https://xsoar.pan.dev/docs/reference/index).

When setting up an instance, you can configure the integration instance to fetch events. You can also set the interval for which to fetch new issues by configuring the **Issue Fetch Interval** field. The fetch interval default is 1 minute. This enables you to control the interval in which an integration instance reaches out to third-party platforms to fetch issues into Cortex XSIAM.

{% hint style="info" %}
### Note

* In some integrations, the **Issue Fetch interval** is called **Feed Fetch Interval**.
* If the integration instance does not have the **Issue Fetch Interval** field, you need to add this field by editing the integration settings. If the integration is from a content pack, you need to create a copy of the integration. Any future updates to this integration will not be applied to the copy integration.
* If you turn off fetching for a while and then turn it on or disable the instance and enable it, the instance remembers the last run and pulls all events that occurred while it was off. If you don't want this to happen, verify that the instance is enabled and click **Reset the “last run” timestamp** when editing the instance. Also, note that "last run" is retained when an instance is renamed.
{% endhint %}

After configuring the instance, you may need to set up a correlation rule to ingest issues.

Correlation rules are predefined logic or patterns that Cortex XSIAM uses to identify relationships between disparate events occurring across an organization's IT environment. If the conditions specified in the rule are met, Cortex XSIAM generates an issue.

**How to fetch issues**

1. Navigate to **Settings** → **Data Sources & Integrations**, find and select the integration, and click **Add Instance**.
2.  In the integration's dialog box, select **Fetch issues**.

    After this setting is enabled, Cortex XSIAM searches for events that occurred within the time frame set for the integration, which is based on the specific integration. The default is 10 minutes, but it can be changed in the integration script.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>To authenticate the fetch, you must select a valid credential. If your user role has the <strong>Credentials</strong> permission set to <strong>None</strong>, you will not be able to select pre-saved credentials. Instead, the message <strong>Credentials are locked by admin</strong> is displayed. In this case, you must manually enter the authentication details or ensure your role has at least <strong>View</strong> permissions for the <strong>Credentials</strong> component.</p></div>
3. (Optional) In the **Issue Fetch Interval** field, set the interval of hours and minutes to fetch alerts (default 1 minute).
4.  (Optional) If the **Issue Fetch Interval** field does not appear, add it to the integration.

    Relevant for any issue fetching integration:

    1.  For integrations installed from a content pack, select the duplicate integration button.

        If you have already duplicated the integration, click the Edit integration’s source button.
    2.  In the **Basic** section, select the **Fetch issues** checkbox.

        In the **Parameters** section, you can see that the **`IssueFetchInterval`** parameter is added. Change the default value if necessary.
    3. Click **Save** to save the changes.
5.  To generate issues, add correlation rules, as required.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Some content packs include preconfigured correlation rules, but you should review them to see if they suit your use case and duplicate them if required. Go to <strong>Threat Management</strong> → <strong>Detection Rules</strong> → <strong>Correlations</strong>, search for the relevant rule, right-click, and select <strong>Preview Rule</strong>. For example, the <strong>ServiceNow v2 Alerts (automatically generated)</strong> correlation rule uses the following XQL Query:</p><pre class="language-programlisting"><code class="lang-programlisting">dataset = servicenow_v2_generic_alert_raw
    | filter _alert_data != null
    | alter alert_severity = json_extract_scalar(_alert_data, "$.severity")
    | alter alert_category = json_extract_scalar(_alert_data, "$.alert_category")
    | alter alert_name = json_extract_scalar(_alert_data, "$.alert_name")
    | alter alert_description = json_extract_scalar(_alert_data, "$.alert_description")
    </code></pre><p>You may want to update the query by defining complex, multi-source detection logic or add filters, such as alert severity or assignee.</p></div>
