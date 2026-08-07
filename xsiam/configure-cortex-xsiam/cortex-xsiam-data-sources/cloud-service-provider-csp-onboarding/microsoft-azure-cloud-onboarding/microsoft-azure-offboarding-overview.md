---
description: >-
  This section contains the technical procedures required to safely decommission
  and offboard your Cortex XSIAM resources in Microsoft Azure.
---

# Microsoft Azure offboarding overview

When you delete an Azure cloud instance from Cortex XSIAM, the cloud instance is removed from the platform. However, the Azure resources created during onboarding, including role assignments, role definitions, diagnostic settings, deployment stacks, resource groups, and managed identities, remain in your Azure environment until you explicitly clean them up.

The offboarding method depends on two factors:

* The scope at which the cloud instance was onboarded (subscription, management group, tenant, or tenant with Entra ID only).
* The template type used during onboarding (ARM or Terraform).

Use the table below to identify the correct offboarding procedure for your Microsoft Azure cloud instance.

<table><thead><tr><th width="205.2265625">Onboarding scope</th><th width="145.54296875">Template type</th><th>Procedure</th></tr></thead><tbody><tr><td>All scopes</td><td>Terraform</td><td><a href="microsoft-azure-offboarding-overview/offboard-terraform-based-azure-deployments-all-scopes">Offboard Terraform-based Azure deployments (all scopes)</a></td></tr><tr><td>Subscription</td><td>ARM</td><td><a href="microsoft-azure-offboarding-overview/offboard-azure-subscription-arm">Offboard Azure subscription (ARM)</a></td></tr><tr><td>Management group or tenant</td><td>ARM</td><td><a href="microsoft-azure-offboarding-overview/offboard-azure-management-group-or-tenant-scope-arm">Offboard Azure management group or tenant scope (ARM)</a></td></tr><tr><td>Tenant (Entra ID only)</td><td>ARM</td><td><a href="microsoft-azure-offboarding-overview/offboard-azure-tenant-with-entra-id-only">Offboard Azure tenant with Entra ID only</a></td></tr></tbody></table>
