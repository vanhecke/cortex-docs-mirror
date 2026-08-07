# Multi-tenant central licensing management

The new central licensing management for MSSP and enterprise multi-tenant allows the MSSP or enterprise to own and manage their child tenants dynamically from the Cortex Gateway. The Cortex Gateway displays the main account with its child tenants and the number of endpoints , employees, and GBs available to allocate to child tenants. The Admin user of the main account can add and delete child tenants, edit allocation of resources to child tenants, and change the child tenant subdomain.

The following are the minimum license requirements for central licensing management:

| Option                  | Description                                                                                                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MSSP multi-tenant       | A multi-tenant deployment enables MSSPs to centrally manage multiple tenants and their resources from the Cortex Gateway.                                                      |
| Enterprise multi-tenant | Large enterprises can have many subdivisions and want to manage their tenant allocation and resources centrally from a main tenant while maintaining complete data separation. |

{% hint style="info" %}
### Note

In MSSP or enterprise multi-tenant, the license specifies the maximum number of child tenants that can be created. Once this limit is reached, no additional tenants can be created, even if there remains allocation for endpoints or GBs.
{% endhint %}
