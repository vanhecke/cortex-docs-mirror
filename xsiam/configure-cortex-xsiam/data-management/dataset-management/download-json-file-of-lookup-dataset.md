# Download JSON file of lookup dataset

{% hint style="warning" %}
### Prerequisite

Dataset Management requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Event Forwarding.
{% endhint %}

You can only download a JSON file for a lookup dataset, where the **Type** set to **Lookup** on the **Dataset Management** page. This option is not available for any other dataset type.

When you download a lookup dataset with field names in a foreign language, the downloaded JSON file displays the fields as `COL_<randomstring>` as opposed to returning the fields in the foreign language as expected.

1. Open the **Settings** → **Configurations** → **Data Management** → **Dataset Management** page.
2. In the **Datasets** table, right-click the lookup dataset that you want to download as a JSON file, and select **Download**.
