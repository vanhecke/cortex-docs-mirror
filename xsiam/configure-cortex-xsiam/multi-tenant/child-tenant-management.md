---
description: >-
  Manage Cortex XSIAM child tenants from a parent tenant by investigating their
  data and applying centralized security configurations.
---

# Child tenant management

You can manage, track, and investigate child tenant data from the parent tenant.

### Manage a child tenant in Cortex XSIAM

Multi-tenancy enables you to view and investigate Cortex XSIAM data of a child tenant and initiate security actions on their behalf.

In Cortex XSIAM, you have access to view the following pages:

* Cases
* Issues
* Query Builder
* Query Center and Results
* Causality View
* Timeline View

To initiate security actions on your child tenant, you need to create a **Configuration**. Security actions are managed by configurations you create in Cortex XSIAM and then assign to each of the child tenants. Each action requires its own configuration and allocation to a child tenant.

{% hint style="info" %}
Once a configuration is created, Cortex XSIAM resets the child tenant data and synchronizes the security actions configured in the parent tenant.
{% endhint %}

You can create configurations for the following actions:

* Starred Issue Policies
* Issue Exclusions
* Profiles
* Allow/Block Lists
