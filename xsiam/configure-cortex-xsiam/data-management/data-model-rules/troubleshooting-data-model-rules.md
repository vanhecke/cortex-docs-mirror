# Troubleshooting Data Model Rules

{% hint style="warning" %}
### Prerequisite

Data Model Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Parsing Rules, and Event Forwarding.
{% endhint %}

To help you easily identify and resolve errors related to invalid Cortex Data Model (XDM) Rules, Cortex XSIAM provides the following:

* When an XDM query runs and one of the Data Model Rules is invalid, the invalid rule is automatically disabled and excluded from the query, and a warning is displayed.
* When a Data Model Rule is disabled, a message is added to your Cortex XSIAM console Notification Center. For more information about the Data Model Rules notifications, see [Data Model Rules notifications](data-model-rules-notifications).
* The Data Model Rules editor displays an error icon and a message beside invalid Data Model Rules.
*   An audit log is added to the Management Audit Log whenever a Data Model Rule becomes invalid, and when an invalid Data Model Rule becomes valid.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>To ensure you and your colleagues stay informed about Data Model Rules activity, you can also <a href="../../../onboard-cortex-xsiam/post-deployment/data-and-log-forwarding/forward-logs-and-data-from-cortex-xsiam-to-external-services/configure-notification-forwarding">Configure notification forwarding</a> to forward your Data Model Rules audit logs to an email distribution list or Syslog server. For more information about the Data Model Rules audit logs, see <a href="monitor-data-model-rules-activity">Monitor Data Model Rules activity</a>.</p></div>
* When a rule is fixed, it is automatically enabled. User defined Data Model Rules are updated manually in the User Defined Rules editor. While default Data Model Rules are updated as part of a Marketplace package update, or a background change, such as an XQL content change.
* All Data Model Rules compilation errors are added to the `parsing_rules_errors` dataset.

**Dataset for Data Model Rules Errors**

All Data Model Rules compilation errors, such as syntax errors, missing arguments, and invalid regex, are saved to a dataset called `parsing_rules_errors`. This dataset also includes Parsing Rules errors. The following table describes the fields that are applicable to troubleshooting Data Model Rules errors when running a query in XQL Search for the `parsing_rules_errors` dataset in alphabetical order.

{% hint style="info" %}
### Note

Since this dataset also contains Parsing Rules errors, some of the fields are irrelevant for Data Model Rules and aren't included in the table.
{% endhint %}

<details>

<summary>Read more...</summary>

| Field           | Description                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------- |
| CREATED\_AT     | Displays the timestamp when the error was generated.                                                                |
| ERROR\_CATEGORY | Displays the category of the error, which for Data Model Rules errors is always **Compile** for compilation errors. |
| ERROR\_MESSAGE  | Displays the error message.                                                                                         |
| \_ID            | Displays the Rule ID that triggered this error.                                                                     |
| RULE\_TYPE      | Displays the type of rule that triggered this error.                                                                |
| TARGET\_DATASET | Displays the target dataset associated to the rule that triggered this error.                                       |
| \_TIME          | Displays the timestamp when the error was generated.                                                                |
| XQL\_TEXT       | Displays the specific section of the Data Model Rule related to the error generated.                                |

</details>
