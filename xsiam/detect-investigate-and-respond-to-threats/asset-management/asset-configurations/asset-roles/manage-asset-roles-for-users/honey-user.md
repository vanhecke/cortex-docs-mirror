# Honey user

{% hint style="warning" %}
### Prerequisite

The honey user role is available only if the Identity Threat Module add-on is enabled.
{% endhint %}

A honey user is a decoy account designed to mimic a legitimate user within your environment. This kind of user looks attractive to potential attackers, with access to many assets, and is used for triggering alerts if accessed.

One of the techniques used by an attacker trying to gain access to your network is attempting to use the credentials of accounts in your organization. By setting up honey users, you can detect these access attempts as soon as they occur. Unlike genuine user accounts, honey users have no legitimate purpose within the organization, making any activity involving them inherently suspicious. Cortex XSIAM uses its out-of-the-box Identity Threat Module to automatically detect activity on the honey user role for identifying suspicious activities.

To use a honey user account for detection, you must configure it manually.

**Configure a honey user**

1. In **Inventory** → **Assets** → **Configurations** → **Asset Roles,** right click to select **Honey User**.
2. Click **Edit Asset Role**.
3. Select **Add User** → **Add New** and enter the honey user account details in the NetBIOS\SAM Account format.
