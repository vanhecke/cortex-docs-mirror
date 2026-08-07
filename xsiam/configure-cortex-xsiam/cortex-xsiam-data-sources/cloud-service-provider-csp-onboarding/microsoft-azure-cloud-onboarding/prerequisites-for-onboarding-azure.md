---
description: >-
  Before you begin onboarding Microsoft Azure, you must review the following
  prerequisites.
---

# Prerequisites for onboarding Azure

## Permissions

Before you begin to onboard Microsoft Azure to Cortex XSIAM, ensure that you have the necessary permissions:

* In Cortex XSIAM, you must have a Cortex XSIAM role with Data Sources - View & Edit permissions (to add/configure cloud accounts in Cortex XSIAM). This role is included in the following built-in roles: Instance Administrator, Security Admin, and IT Admin.
* In Microsoft Azure, you must have an admin user with the [required permissions](#required-azure-permissions-for-cortex-xsiam-onboarding).

## Additional prerequisites

Before you begin onboarding Microsoft Azure, ensure that:

* You have a Microsoft Azure subscription.
* You obtain the tenant ID and subscription ID. You can view these in the Microsoft Azure Portal in Management groups.

### Custom (user-defined) audit log collection

If you are configuring custom (user-defined) audit log collection using an existing Event Hub, ensure that:

* You have the Event Hub name, Event Hub namespace, and Event Hub resource group name.
* The namespace and Event Hub belong to the specific Azure subscription being onboarded. Cross-subscription or centralized logging is not currently supported.

## Required Azure permissions for Cortex XSIAM onboarding

This section lists all Azure permissions required for Cortex XSIAM onboarding using custom roles (least-privilege). It covers both the Terraform (TF) and ARM (onboard.sh) provisioning methods. The specific permissions required depend on your target scope (subscription, management group, or tenant) and whether audit log collection is enabled.

### Global permission prerequisites for creating service principal

When onboarding an Azure tenant to Cortex XSIAM, the onboarding wizard automatically checks for the Cortex service principal when you enter your Azure tenant ID. If the service principal is missing, the wizard provides a command to register it manually, establishing Cortex XSIAM's primary runtime identity within your Azure tenant so you can proceed with onboarding. The user who runs the command to create the service principal must have the **Application Administrator** built-in Entra ID role.

### Overview of required Azure permissions by onboarding scope

Find your target scope below to see the required roles you need to assign or create.

<table data-header-hidden><thead><tr><th width="135.3125"></th><th></th><th></th></tr></thead><tbody><tr><td>Onboarding scope</td><td>Base permissions required</td><td>Additional permissions required if audit log collection is enabled</td></tr><tr><td>Subscription</td><td>Create the <a href="#basic-subscription-custom-role-permissions">Basic Subscription</a> custom role (using the permissions listed below) and assign it at the target subscription.</td><td>Create the <a href="#audit-log-collection-custom-role-permissions">Audit Log Collection</a> custom role (using the permissions listed below) and assign it at the target subscription.</td></tr><tr><td>Management group</td><td><ol><li>Assign the <a href="#basic-subscription-custom-role-permissions">Basic Subscription</a> role. Create a custom <a href="#basic-management-group-custom-role-permissions">Basic Management Group</a> role (using the permissions listed below) and assign it at the target management group.</li><li>Assign the built-in <strong>Privileged Role Administrator</strong> Entra ID role and the <strong>Application Administrator</strong> Entra ID role.</li></ol></td><td>Create the <a href="#audit-log-collection-custom-role-permissions">Audit Log Collection</a> custom role (using the permissions listed below) and assign it at the target management group.</td></tr><tr><td>Tenant</td><td><ol><li>Assign the <a href="#basic-subscription-custom-role-permissions">Basic Subscription</a> role. Create a custom <a href="#basic-management-group-custom-role-permissions">Basic Management Group</a> role (using the permissions listed below) and assign it at the root management group.</li><li>Assign the built-in <strong>Privileged Role Administrator</strong> Entra ID role and the <strong>Application Administrator</strong> Entra ID role.</li></ol></td><td><ul><li>Create the <a href="#audit-log-collection-custom-role-permissions">Audit Log Collection</a> custom role (using the permissions listed below) and assign it at the target management group.</li><li>Assign the built-in <strong>Security Admin</strong> Entra ID role (required for updating/destroying diagnostic settings).</li></ul></td></tr></tbody></table>

#### Basic Subscription custom role permissions

These permissions must be included in a custom Azure role assigned at the subscription level.

```
Microsoft.Resources/deploymentScripts/delete
Microsoft.Resources/deploymentScripts/logs/read
Microsoft.Resources/deploymentScripts/read
Microsoft.Resources/deploymentScripts/write
Microsoft.Resources/deployments/delete
Microsoft.Resources/deployments/operations/read
Microsoft.Resources/deployments/operationstatuses/read
Microsoft.Resources/deployments/read
Microsoft.Resources/deployments/validate/action
Microsoft.Resources/deployments/whatIf/action
Microsoft.Resources/deployments/write
Microsoft.Resources/subscriptions/resourceGroups/delete
Microsoft.Resources/subscriptions/resourceGroups/read
Microsoft.Resources/subscriptions/resourceGroups/write
Microsoft.Authorization/roleAssignments/delete
Microsoft.Authorization/roleAssignments/read
Microsoft.Authorization/roleAssignments/write
Microsoft.Authorization/roleDefinitions/delete
Microsoft.Authorization/roleDefinitions/read
Microsoft.Authorization/roleDefinitions/write
Microsoft.ContainerInstance/containerGroups/delete
Microsoft.ContainerInstance/containerGroups/read
Microsoft.ContainerInstance/containerGroups/write
Microsoft.ManagedIdentity/userAssignedIdentities/assign/action
Microsoft.ManagedIdentity/userAssignedIdentities/delete
Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials/delete
Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials/read
Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials/write
Microsoft.ManagedIdentity/userAssignedIdentities/read
Microsoft.ManagedIdentity/userAssignedIdentities/write

```

#### Basic Management Group custom role permissions

These permissions must be included in a custom Azure role assigned at the management group level. Assign this role in addition to the basic subscription layer.

```
Microsoft.Management/managementGroups/read
Microsoft.Authorization/policyAssignments/delete
Microsoft.Authorization/policyAssignments/read
Microsoft.Authorization/policyAssignments/write
Microsoft.Authorization/policyDefinitions/delete
Microsoft.Authorization/policyDefinitions/read
Microsoft.Authorization/policyDefinitions/write
Microsoft.Compute/galleries/write
Microsoft.Compute/galleries/read
Microsoft.Resources/deploymentStacks/validate/action
Microsoft.Resources/deploymentStacks/write
Microsoft.Resources/deploymentStacks/read
Microsoft.Resources/deploymentStacks/delete
Microsoft.Resources/deploymentStacks/exportTemplate/action
Microsoft.Resources/deploymentStacks/manageDenySetting/action
Microsoft.Resources/deploymentStacksWhatIfResults/read
Microsoft.Resources/deploymentStacksWhatIfResults/write
Microsoft.Resources/deploymentStacksWhatIfResults/delete
Microsoft.Resources/deploymentStacksWhatIfResults/whatIf/action

```

#### Audit Log Collection custom role permissions

These permissions must be included in a custom Azure role assigned at the target scope. Assign this role in addition to the previous roles according to the scope being onboarded.

```
Microsoft.EventHub/namespaces/authorizationRules/delete
Microsoft.EventHub/namespaces/authorizationRules/listKeys/action
Microsoft.EventHub/namespaces/authorizationRules/read
Microsoft.EventHub/namespaces/authorizationRules/write
Microsoft.EventHub/namespaces/delete
Microsoft.EventHub/namespaces/eventhubs/consumergroups/delete
Microsoft.EventHub/namespaces/eventhubs/consumergroups/read
Microsoft.EventHub/namespaces/eventhubs/consumergroups/write
Microsoft.EventHub/namespaces/eventhubs/delete
Microsoft.EventHub/namespaces/eventhubs/read
Microsoft.EventHub/namespaces/eventhubs/write
Microsoft.EventHub/namespaces/networkRuleSets/read
Microsoft.EventHub/namespaces/read
Microsoft.EventHub/namespaces/write
Microsoft.Insights/diagnosticSettings/delete
Microsoft.Insights/diagnosticSettings/read
Microsoft.Insights/diagnosticSettings/write
Microsoft.PolicyInsights/remediations/delete
Microsoft.PolicyInsights/remediations/read
Microsoft.PolicyInsights/remediations/write
Microsoft.Storage/storageAccounts/blobServices/containers/delete
Microsoft.Storage/storageAccounts/blobServices/containers/read
Microsoft.Storage/storageAccounts/blobServices/containers/write
Microsoft.Storage/storageAccounts/blobServices/read
Microsoft.Storage/storageAccounts/delete
Microsoft.Storage/storageAccounts/fileServices/read
Microsoft.Storage/storageAccounts/listKeys/action
Microsoft.Storage/storageAccounts/read
Microsoft.Storage/storageAccounts/write
microsoft.aadiam/diagnosticsettings/delete
microsoft.aadiam/diagnosticsettings/read
microsoft.aadiam/diagnosticsettings/write
Microsoft.EventHub/namespaces/networkRuleSets/write
Microsoft.Storage/storageAccounts/blobServices/write
Microsoft.EventHub/namespaces/eventhubs/authorizationRules/read
Microsoft.EventHub/namespaces/eventhubs/authorizationRules/write
Microsoft.EventHub/namespaces/eventhubs/authorizationRules/listKeys/action
microsoft.directory/servicePrincipals/delete

```

### Audit log collection in a tenant scope: Entra ID role requirement

This section applies when audit log collection is enabled and the onboarding is done at the tenant scope.

The `microsoft.aadiam/diagnosticSettings` permissions family at the tenant level is required for provisioning relevant resources required for audit log collection. The onboarding user must have the Security Administrator Entra ID role (or Global Administrator) in order to create, update, and delete the Azure diagnostic settings.

For more information, see [Microsoft documentation](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-configure-diagnostic-settings).
