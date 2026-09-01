---
description: Use OpenLDAP authentication for Cortex XSIAM.
---

# OpenLDAP

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

This connector is available with any active Cortex XSIAM or Cortex AgentiX license.

Use your OpenLDAP or Active Directory user authentication settings to log in to Cortex XSOAR. Users log in with their OpenLDAP or Active Directory username and password, and their permissions are set according to the groups and mapping defined in AD Roles Mapping. For connecting to the LDAP server with a TLS connection, it is recommended to use this integration instead of the Active Directory Authentication server integration.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [OpenLDAP](https://xsoar.pan.dev/docs/reference/integrations/open-ldap): Authenticate using OpenLDAP or Active Directory.

To configure this connector, follow the steps outlined in the configuration wizard.
