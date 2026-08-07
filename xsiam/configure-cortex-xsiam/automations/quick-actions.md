# Quick Actions

Quick Actions are preset single commands that enable you to automate basic tasks such as creating tickets in third-party systems, sending Slack messages, and changing issue severity.

You can use quick actions for the following:

* **Automation rules**: You can create predefined rules to run Quick Actions as issues are created. For more information, see [Create an automation rule](create-an-automation-rule)
* **Manual execution**: When investigating an issue, in the **Issues** table, you can right-click to **Run an Automation** on one or more issues. For more information, see [Run an automation on an issue](../../detect-investigate-and-respond-to-threats/investigation-and-response/investigate-issues/run-an-automation-on-an-issue).

By default, Quick Actions run using all available integration instances that contain the command. When selecting a Quick Action to run on an issue or to use for an automation rule, you can also choose one specific integration instance.

When you run an automation from the **Issues** table, in some cases the system provides recommended Quick Actions, based on the context. Quick Actions may also be provided in Recommended Automation Rules.

{% hint style="info" %}
### Note

Quick Actions appear as War Room entries, but do not appear in the Work Plan.
{% endhint %}

**Access attributes in the Unified Asset Inventory**

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

Quick Actions can automatically populate parameters such as region, account id, and tags, based on asset data. When a Quick Action is triggered manually by a user or automatically through an automation rule, it can reference UIA attributes for the relevant asset(s) in the issue context and use those attributes as input. The issue must contain the relevant `Asset ID`.

The syntax to reference attributes in the UAI is `${asset.xdm.asset.attributename}`. To find the property path in the XDM data set, see the asset data card for the asset in the **Inventory** page. For example, to print the region for the asset, enter `!print value=${asset.xdm.asset.cloud.region}`. You can also run Quick Actions directly on the asset using `${asset.xdm.asset}`.
