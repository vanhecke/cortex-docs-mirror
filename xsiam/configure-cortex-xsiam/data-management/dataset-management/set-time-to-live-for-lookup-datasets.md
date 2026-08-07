# Set time to live for lookup datasets

{% hint style="warning" %}
### Prerequisite

Dataset Management requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Event Forwarding.
{% endhint %}

You can specify when lookup entries expire and are removed automatically from the lookup dataset by configuring the time to live (TTL). The time period of the TTL interval is based on when the data was last updated. The default is forever and the entries never expire. You can also configure a specific time according to the days, hours, and minutes. Expired elements are removed from the lookup dataset by a scheduled job that runs every five minutes.

1. Open the **Settings** → **Configurations** → **Data Management** → **Dataset Management** page.
2. In the **Datasets** table, right-click the lookup dataset, and select **Set TTL**.
3. Select one of the following to configure when lookup dataset entries expire and are removed:
   * **Forever**: Lookup entries never expire (default).
   * **Custom**: Lookup entries expire according to a set number of days, hours, and minutes. The maximum number of days is 99999.
4.  Click **Save**.

    The **TTL** column in the **Datasets** table is updated with the changes and these changes are applied immediately on all existing lookup entries.
