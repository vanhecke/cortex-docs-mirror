---
description: >-
  You can customize your own Azure outpost by bringing your own app (BYOA). This
  page lists the prerequisites that must be met before customizing your outpost
  in this way.
---

# Task 1: Meet the prerequisites for Azure BYOA outposts

This page lists the prerequisites and permission requirements for deploying an Azure outpost in Bring Your Own App registration (BYOA) mode.

Complete the checks below before you start the deployment procedure, whether you use the recommended shell script or the manual Azure portal path.

{% hint style="info" %}
**Important:** Before you begin, ensure that you have Cortex XSIAM console access with the outpost creation entitlement.
{% endhint %}

## Step 1. Recognize the identities involved in BYOA outpost deployment

The following distinct identities are involved in BYOA deployment.

* **App Registration Creator**: The user that initially sets up the app registration and service principal (either by [running a script](the-shell-script-for-azure-app-registration) or [manually using the Azure portal](../task-2-create-the-app-registration-for-the-azure-byoa-outpost#manually-in-the-azure-portal)).\
  \
  Ensure the identity that runs the setup script or performs the manual Azure portal steps holds the `Application Developer` role (or higher) on the tenant.
* **Terraform Runner Identity**: The Azure identity that deploys the outpost by executing `terraform apply`, and the same identity used for all future outpost upgrades. This can be either a user account (for example, an administrator signed in via `az login`) or a service principal that an authorized user impersonates. In either case, the identity must have the required permissions to create and manage the outpost's Azure resources.\
  \
  Ensure you have the object ID of the Terraform Runner Identity that executes `terraform apply`. You can retrieve the ID by running this command: `az ad sp show --id <client-id> --query id -o tsv`

{% hint style="info" %}
**Tip**: Confusing which permissions are needed by which identity is the most common cause of deployment failure.
{% endhint %}

## Step 2. Meet the tooling and account prerequisites

Confirm that the tooling and account requirements below are in place before you start any BYOA deployment path.

* **Azure CLI**: Version 2.x or later (for the recommended shell script approach), or Azure Portal access (for manual setup)
* **Terraform**: Version specified in the outpost bundle
* **Cortex XSIAM account**: Active account with Azure Outpost entitlement
* **Azure subscription**: A dedicated Azure subscription for the outpost. The subscription should not contain other workloads and should be free of other resources.
* **Entra ID tenant:** Identify the Entra ID tenant where you want the app registration to live. This is the "home tenant" that hosts (or trusts) the Azure subscriptions Cortex XSIAM scans. Do not create the app registration in a separate monitored-workload tenant, because Cortex authenticates from the home tenant into the monitored subscription.

## Step 3. Set permissions by identity

The permissions your identities need differ by role and by lifecycle stage. Review the tables below to confirm that the App Registration Creator has the setup-time permissions and that the Terraform Runner Identity has the persistent deploy-and-upgrade permissions.

### App Registration Creator permissions

The following permissions are needed only during initial setup. You can revoke the access that these permissions grant after setup.

| Role / permission                                                                                                                                                                                                                              | Scope           | Why needed                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Application Developer (primary)</p><p>OR<br><br>Application Administrator (as required only for adding a service principal as an owner of the app registration)</p><p><br>OR</p><p>Global Administrator (sufficient but overprivileged)</p> | Entra ID tenant | <p>Create the app registration and service principal.</p><p>Add owners</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Privileged Role Administrator (optional)                                                                                                                                                                                                       | Entra ID tenant | <p>Required only if granting the optional <code>Application.Read.All</code> admin consent for Entra ID app inventory.<br><br>The optional <code>Application.Read.All</code> admin consent enables Cortex's Entra ID application inventory feature, which discovers and displays all app registrations and enterprise applications in your Entra ID tenant so you can see which applications have access to your Azure resources and detect over-privileged or unused apps. If you do not need this inventory, skip the Privileged Role Administrator role. The outpost itself deploys and scans normally without it.</p> |

### Terraform Runner Identity permissions

The following permissions are persistent and must remain in place for the life of the outpost. They are relevant during deployment and when upgrading.

| Role / permission                                                     | Scope                           | Why needed                                                                                                                             |
| --------------------------------------------------------------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Owner of the BYO App Registration                                     | Object-scoped (one AppReg only) | Add and/or remove federated identity credentials (FICs). Granted automatically by the setup script via `--tf-runner-object-id <GUID>`. |
| Contributor (or Owner, which also includes User Access Administrator) | Azure subscription              | Provision outpost infrastructure: UAMIs, storage, networking, scanner VMs                                                              |
| User Access Administrator (or Owner, which also includes Contributor) | Azure subscription              | Create role assignments between UAMIs and scanned resources                                                                            |

{% hint style="info" %}
**Note**: BYOA mode leverages a least-privilege security model by eliminating the need for tenant-level Microsoft Graph permissions. The Terraform runner service principal modifies the app registration and writes federated identity credentials strictly through direct object ownership. This ownership-based approach ensures secure resource isolation, keeping the app registration strictly scoped to its own environment so it does not read or enumerate other tenant applications. By relying on ownership rather than directory permissions, BYOA bypasses the need for tenant-level admin consent (such as `Application.ReadWrite.OwnedBy`), offering a highly secure alternative to the `Application.ReadWrite.All` permission used by standard outposts.
{% endhint %}

## What's next?

If you encounter issues, review the [outpost troubleshooting topic](../../outpost-troubleshooting#bring-your-own-app-byoa-troubleshooting---azure).

Proceed to [Task 2: Create the app registration for the Azure BYOA outpost](task-2-create-the-app-registration-for-the-azure-byoa-outpost).
