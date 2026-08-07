# Create Data Model Rules

{% hint style="warning" %}
### Prerequisite

Data Model Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Parsing Rules, and Event Forwarding.
{% endhint %}

You can override rules or create your own rules using XQL and additional custom syntax that is specific to defining Data Model Rules. Once you edit a default data model mapping, you will no longer receive Marketplace updates.

Review the following:

* [Data Model Rules editor views](data-model-rules-editor-views)
* [Data Model Rules file structure and syntax](data-model-rules-file-structure-and-syntax)
* [How to map authentication story events?](how-to-map-authentication-story-events)

How to create Data Model Rules

1. In Cortex XSIAM, select **Settings** → **Configurations** → **Data Management** → **Data Model Rules**.
2.  Select the Data Model editor view for writing your Data Model Rules.

    You can select one of the following views:

    * **User Defined Rules**: Leave the default view open and write your Data Model Rules directly in the editor.
    * **Both**: Select this view to see the Data Model Rules editor as well as the default rules as you write your Data Model Rules.
3. Write your rules using XQL syntax and the syntax specific to Data Model Rules.
4.  (Optional) Use XQL Search to test your Data Model Rules and review logs.

    You can create queries on the data model. For more information, see [Create XQL query](../../../detect-investigate-and-respond-to-threats/investigation-and-response/build-xql-queries/how-to-build-xql-queries/create-xql-query).
