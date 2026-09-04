---
description: >-
  Manage permission updates for your cloud instances following new feature
  releases or bug fixes in Cortex XSIAM.
---

# Update cloud permissions after Cortex XSIAM release updates

This topic provides guidance on how to manage permission updates for your cloud instances following new feature releases or bug fixes. It outlines how users are notified of required permission changes and provides step-by-step instructions for granting necessary permissions to ensure continued functionality and security.

{% hint style="info" %}
#### Prerequisites

* Ensure that the user account used to modify permissions has the necessary privileges within both the Cortex platform and your cloud environment, for example, AWS or Azure.
* You received a notification regarding a new version available that requires permission updates, or viewed a **Needs Update** status in the **Data Sources & Integrations** page.
{% endhint %}

1. Navigate to the **Data Sources & Integrations** page.
2. Do the following to identify instances requiring updates:
   1. For the relevant instance, locate the **Update Status** column.
   2. Filter or sort by this column to quickly identify instances marked as **Needs Update**. The message on the page indicates the number of instances that need updating.

{% hint style="info" %}
#### Note

Instances requiring updates will not change their connection status, for example, Connected, Warning, Error, Disabled, due to the pending permission update.
{% endhint %}

1. Do the following to access the connector's permissions section:
   1. Click the name of the specific cloud connector instance that requires permission updates. The connector's detailed view appears.
   2. Within the connector's detailed view, locate and select the permissions section.
2. Review missing permissions. In the permissions section, the missing permission names or changes in permission scope is indicated.
3. Follow the on-screen instructions to grant the required permissions, or refer to the specific permission names or scopes provided.
4. After making the necessary permission adjustments, click **Save** or **Apply Changes** within the connector's configuration.
5. Return to the **Data Sources & Integrations** page and verify that the updated status of the instance shows as up-to-date, or the update is in progress.
6.  Monitor the instance's health and functionality to confirm the changes have taken effect and the connector is operating as expected.

    If you encounter issues during the permission update process, check the generated health alerts for more specific details.
