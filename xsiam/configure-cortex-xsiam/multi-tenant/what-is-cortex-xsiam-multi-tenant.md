---
description: >-
  Learn how Cortex XSIAM multi-tenant deployments isolate child tenant data
  while centralizing licensing, administration, and alert visibility.
---

# What is Cortex XSIAM multi-tenant?

Cortex XSIAM multi-tenant is designed for managed security service providers (MSSPs) and enterprises that require strict data segregation, but also need the flexibility to share and manage critical security practices across tenants. In Cortex XSIAM, MSSPs and enterprises can benefit from central licensing management and have access to a variety of configuration options for their child tenants. These options include defining which Cortex add-ons to include and configuring the number of endpoints and gigabytes per tenant. This flexibility allows multi-tenants to tailor security operations to meet the specific needs of each child tenant.

Multi-tenancy enables you to manage multiple tenants from a single console. For a multi-tenant deployment, you create and manage the main account and child tenants from the Cortex Gateway.

In the main account, you can see all alerts across all child tenants.

### **Multi-tenant architecture in Cortex XSIAM**

Multi-tenancy architecture is based on the platform's ability to run separate instances (process and data) of Cortex XSIAM, linking each child tenant to a main tenant. Each deployment consists of a main account and child tenants. All child tenants are associated with the main tenant. While tenant alerts can be searched from the main tenant, no data is stored on the main tenant.

| Component    | Description                                                                                                                                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Main tenant  | The main tenant, also referred to as the parent tenant, is used to access and administer your environment.                                                                                                               |
| Child tenant | A child tenant is an instance of Cortex XSIAM that serves an end customer, such as the customer of an MSSP, and is associated with the main tenant. Each tenant has customer-specific data, which are stored separately. |

{% hint style="info" %}
### Note

By default, multi-tenant licenses include one child tenant.
{% endhint %}
