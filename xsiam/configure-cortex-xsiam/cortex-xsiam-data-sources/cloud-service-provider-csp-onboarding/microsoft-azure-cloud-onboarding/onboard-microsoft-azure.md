---
description: >-
  Follow the Azure onboarding wizard, and Cortex creates a custom authentication
  template to be executed in Azure.
---

# Onboard Microsoft Azure

Use the cloud onboarding wizard to integrate a Microsoft Azure environment with Cortex XSIAM. The onboarding wizard requires minimal configuration to set up the integration. To complete the minimum configuration, define the scope of the Microsoft Azure accounts and specify the scan mode. Alternatively, configure the advanced settings for full control of the onboarding process.

Cortex XSIAM generates a Terraform or ARM authentication template based on the configuration settings. The authentication template establishes trust with Microsoft Azure. The authentication template also grants required permissions to Cortex XSIAM. Execute the authentication template in Microsoft Azure to complete the onboarding process. Executing the authentication template notifies Cortex XSIAM of the execution details. Cortex XSIAM then creates a new cloud instance.

### Onboard Microsoft Entra ID only

You can onboard Microsoft Entra ID independently of a full tenant-level onboarding. When you select the Onboard Microsoft Entra ID only option during onboarding with Tenant scope, Cortex XSIAM connects to Entra ID to unlock identity-based capabilities, including Cloud Infrastructure Entitlement Management (CIEM), identity posture assessment, and Entra ID sign-in log ingestion. This approach enables identity visibility without requiring Cortex XSIAM to scan or manage the broader Azure tenant environment.

When you onboard Entra ID only, Cortex XSIAM operates in collection-only mode. Scan mode selection and scope modification are not available for this configuration. Both Terraform and ARM authentication templates are supported, and manual onboarding is also available. Cortex XSIAM generates the appropriate authentication template based on your selection, and you execute it in Microsoft Azure to complete the onboarding process.

If you enable audit log collection with Entra ID-only onboarding using automated collection, Cortex XSIAM ingests sign-in and activity log categories including: SignInLogs, AuditLogs, NonInteractiveUserSignInLogs, ServicePrincipalSignInLogs, ManagedIdentitySignInLogs, ProvisioningLogs, ADFSSignInLogs, and MicrosoftGraphActivityLogs. Administrative category logs are excluded from automated collection. If you configure custom diagnostic settings, log ingestion follows your specified configuration.

You can later expand an Entra ID-only configuration to full tenant scope by editing the onboarding configuration. This approach lets you to begin with identity-focused onboarding and transition to comprehensive tenant coverage as requirements evolve.

### About the Cortex XSIAM service principal

A service principal is an identity that an application uses to authenticate and interact with Azure resources. When Cortex XSIAM connects to your Azure tenant, Cortex XSIAM uses a service principal as its runtime identity in that tenant.

Cortex XSIAM uses the service principal to:

* Authenticate to your Azure tenant without requiring interactive user sign-in during ongoing operations.
* Perform the role assignments and resource provisioning defined in the authentication template you execute during onboarding.
* Operate within the custom roles and scoped permissions you grant, following the principle of least privilege.

When you onboard an Azure tenant for the first time, Cortex XSIAM checks automatically whether the Cortex service principal already exists in your tenant when you enter your tenant ID in the onboarding wizard. If the Cortex service principal does not yet exist in your tenant, you must create it before you can proceed with onboarding. Cortex XSIAM displays the Azure CLI command to run in the onboarding wizard. The user who runs this command must have the Application Administrator built-in Entra ID role. The Application Administrator role is required only to create the Cortex service principal. After the service principal exists in your tenant, you do not need this role to complete the rest of the onboarding process.

### Automated deployment per subscription with Azure policy <a href="#automated-deployment-per-subscrpition-with-azure-policy" id="automated-deployment-per-subscrpition-with-azure-policy"></a>

When you onboard an Azure Management Group or Tenant, Cortex XSIAM uses a native Azure Policy with the `deployIfNotExists` effect to keep every subscription under that scope covered automatically, including subscriptions created after onboarding.

**Why Cortex XSIAM deploys into each subscription**

Cortex XSIAM creates a dedicated resource group (`cortex-{suffix}`) in every in-scope subscription. Two Azure constraints drive this:

* **Ephemeral scan resource containment:** Capabilities like DSPM and Agentless Disk Scanning (ADS) generate short-lived artifacts during scans. A dedicated resource group limits write/delete permissions to that group rather than the whole subscription, and gives you a single container for auditing, cost attribution, and cleanup.
* **Scoped role placement:** Some permissions (such as data actions for reading blob or file data) cannot be assigned at the Management Group level due to Azure RBAC constraints. They must be granted at the subscription level, scoped to the Cortex XSIAM resource group where possible.

**How it works**

Cortex XSIAM uses Azure Policy with the `deployIfNotExists` (DINE) effect, a standard first-party Azure capability. During onboarding, Cortex XSIAM creates one custom policy definition and assigns it to your selected Management Group (or Tenant Root Management Group). Azure then evaluates all current and future subscriptions under that scope on its own schedule and deploys any missing Cortex XSIAM resources through its own control plane.

The deployment flow:

1. Azure Policy detects a non-compliant subscription.
2. Azure's Policy control plane launches the embedded deployment using the managed identity (`cortex-mi-{suffix}`) in Incremental mode, adding or updating only Cortex XSIAM resources.
3. The managed identity creates the `cortex-{suffix}` resource group and any per-subscription resources for the enabled capabilities.

`cortex-mi-{suffix}` is a User-Assigned Managed Identity attached only to the policy. It holds the privileged write/delete permissions needed for deployment and is used exclusively by Azure's Policy control plane. Cortex XSIAM has no access to it.

On first onboarding, Cortex XSIAM uses the Service Principal's `remediations/write` permission to trigger an initial re-evaluation. This re-runs the existing remediation logic only and cannot change what gets deployed.

**Microsoft reference documentation:**

* [Azure Policy deployIfNotExists effect](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-deploy-if-not-exists)
* [Remediate non-compliant resources with Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/how-to/remediate-resources)
* [Get Azure Policy compliance data](https://learn.microsoft.com/en-us/azure/governance/policy/how-to/get-compliance-data)

#### **What gets created, and when**

* **Base onboarding (always):** An empty resource group named `cortex-{suffix}` is created in every in-scope subscription.
* **Agentless Disk Scanning (when ADS is enabled):** In addition to the ADS roles and permissions, Cortex XSIAM creates a Compute Gallery named `cortex_ads_{suffix}` inside the `cortex-{suffix}` resource group. This is an empty, no-cost container to hold temporary image versions during scans.

#### **Roles and permissions reference**

For the complete list of permissions and roles created for each capability, see the [Cortex XSIAM Azure Permissions documentation](microsoft-azure-provider-permissions).
