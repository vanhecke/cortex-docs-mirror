---
description: >-
  You can customize your own outpost for Azure by bringing your own app (BYOA).
  This page describes the steps for creating the app registration.
---

# Task 2: Create the app registration for the Azure BYOA outpost

This page describes how to create the Azure Entra ID app registration that a Bring Your Own App (BYOA) outpost uses to authenticate into your monitored Azure subscription. Complete this task after you confirm the prerequisites and before you deploy the outpost.

Create the app registration using one of the following methods:

* [With a shell script (recommended)](#with-a-shell-script-recommended): A helper script runs the required Azure CLI commands in a single command, adds the Terraform runner as an owner of the app registration, and optionally creates the scanner managed identities in a resource group you control. Use this method when you can run bash on your workstation and want the fastest, least error-prone path.
* [Manually in the Azure portal](#manually-in-the-azure-portal): You click through the Microsoft Entra ID blade to create the app registration, copy its identifiers, and add the Terraform runner as an owner. Use this method when you cannot run the shell script (for example, in a portal-only environment) or when your organization requires a visual audit trail of each step. The manual method does not create scanner-managed identities, so Cortex creates them for you during outpost deployment.

## With a shell script (recommended)

Start with this task to deploy a Cortex XSIAM Azure outpost using your own pre-created Entra ID app registration (BYOA).

Run a [helper shell script](the-shell-script-for-azure-app-registration) called `setup-byo-app-registration.sh` that creates the app registration, creates its service principal, and grants the Terraform runner the ownership it needs to attach federated identity credentials later.

{% hint style="info" %}
**Note:** This approach is the preferred alternative to creating the app registration manually in the Azure portal because it completes the required actions in a single command and prevents the most common deployment failures.
{% endhint %}

### Shell script step 1: Decide what the script provisions

What you decide to provision determines the prerequisites, the script arguments, and the items you will need to provide to the Cortex XSIAM wizard. Choose between:

* **App registration only.** The script creates the app registration and its service principal. Cortex creates the scanner managed identities (UAMIs) for you during outpost deployment. This is the default and the right choice for most organizations.
* **App registration and scanner managed identities.** The script creates the app registration and its service principal, and also creates scanner UAMIs (agentless, DSMP, registry, serverless, and proxy) in a resource group that you specify. The script grants the Terraform runner the role assignment it needs to attach the UAMI federated identity credentials. Choose this configuration when your governance policies require that managed identities live in a customer-owned resource group with your own naming conventions, instead of in a Cortex-created resource group.

Later, when [running the script](#shell-script-step-5-run-the-helper-shell-script-terminal), you determine what to provision by adding or omitting certain command flags and arguments.

### Shell script step 2: Before you begin

Before you run the script, confirm that the prerequisites are met. Skipping any of these prerequisites causes the script to fail or causes a later `terraform apply` to fail.

#### Always required

These prerequisites are required whenever you run the script, regardless of what you are provisioning.

* **Azure CLI:** Version 2.x or later, installed on your workstation. The script runs on macOS, Linux, and Windows (via Git Bash or WSL2).
* **Entra ID role:** The identity that runs the script must hold the built-in `Application Developer` role on the tenant where the app registration lives. By default any user can register applications, but if your tenant has disabled user registration, an administrator must grant you this role.
*   **Terraform runner object ID:** The object ID (a GUID) of the identity that runs `terraform apply` for this outpost. This is almost always a service principal, not a human user. You will retrieve the object ID in [Step 3](#shell-script-step-3-look-up-the-terraform-runner-object-id-terminal-azure-cli).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Do not confuse the object ID with the client ID. They are both GUIDs, both are returned by the Azure CLI, and they are not interchangeable.</p></div>
* **Entra ID tenant:** The tenant where you want the app registration to live. This is usually your home tenant, not the tenant that hosts the monitored subscription. The script creates the app registration in whichever tenant your Azure CLI session is signed in to, so signing in to the correct tenant when you perform [Step 4](#shell-script-step-4-sign-in-to-the-correct-entra-id-tenant-terminal-azure-cli) is critical.

#### Also required when creating scanner managed identities

These permissions are required when you also use the script to create scanner managed identities.

* **Azure RBAC roles:** The identity that runs the script must hold either `Owner` on the target subscription, or `Contributor` plus `User Access Administrator` on the target subscription, or the equivalent least-privilege combination on a pre-created resource group. For the least-privilege option, see the script's `README.md`.
* **Subscription, resource group, and region:** The Azure subscription ID where the UAMIs go, the name of the resource group to hold them (the script creates the group if it does not exist), and the Azure region for that resource group (for example, `australiaeast` or `eastus`).

### Shell script step 3: Look up the Terraform runner object ID (terminal, Azure CLI)

The script needs the object ID of the identity that runs `terraform apply` so that it can add that identity as an owner of the new app registration. Open a terminal and run one of the commands below, depending on whether the runner is a service principal or your own user account.

For a service principal (the typical production case):

```sh
az ad sp show --id <sp-client-id> --query id -o tsv
```

For your own user account (testing only):

```sh
az ad signed-in-user show --query id -o tsv
```

Copy the GUID that the command returns. This is the value you will pass to the script in [Step 5](#shell-script-step-5-run-the-helper-shell-script-terminal) as the `--tf-runner-object-id` argument.

### Shell script step 4: Sign in to the correct Entra ID tenant (terminal, Azure CLI)

The script creates the app registration in whichever tenant your Azure CLI session is currently signed in to, so you must sign in to the tenant where the app registration is meant to live. This is usually your home tenant, not the monitored subscription's tenant. If you are also creating scanner managed identities, the same tenant must host the target subscription.

In the same terminal, run:

```sh
az login --tenant <your-tenant-id>
```

After the browser flow completes, verify that the active session is on the correct tenant:

```sh
az account show --query tenantId -o tsv
```

If you are also creating scanner managed identities, set the active subscription to the one where the UAMIs go:

```sh
az account set --subscription <uami-subscription-id>
```

### Shell script step 5: Run the helper shell script (terminal)

The helper shell script is called `setup-byo-app-registration.sh` and can be copied/pasted from [The shell script for Azure app registration](the-shell-script-for-azure-app-registration). A detailed technical reference in the format of a README is also available at that link.

Run the script with the arguments for the provisioning you choose. Use the form for app registration only, or the form for app registration plus scanner managed identities. The script prints progress messages to the terminal as each action completes.

Change into the directory where you created the script, such as:

```sh
cd <customer_managed>/app_registration/
```

#### To create the app registration only

Pass the required arguments: A unique display name for the new app registration, and the Terraform runner object ID you retrieved in [Step 3](#shell-script-step-3-look-up-the-terraform-runner-object-id-terminal-azure-cli).

```sh
./setup-byo-app-registration.sh \
  --app-name <app-display-name> \
  --tf-runner-object-id <tf-runner-object-id>
```

For example:

```sh
./setup-byo-app-registration.sh \
  --app-name cortex-scan-platform-my-subscription \
  --tf-runner-object-id 12345678-1234-1234-1234-123456789abc
```

The script:

* Creates a multi-tenant app registration.
* Creates its service principal.
* Adds the Terraform runner as an owner of the app registration. This is the production path. Without it, the `terraform apply` fails on the first FIC create with HTTP 403: "Insufficient privileges."
* Adds the currently-signed-in user as Owner (best-effort for interactive portal debugging).

#### To also create the scanner managed identities

Pass the same required arguments as for the app-registration-only form, plus the `--add-uamis` flag and additional required arguments that tell the script where to create the UAMIs.

```sh
./setup-byo-app-registration.sh \
  --app-name <app-display-name> \
  --tf-runner-object-id <tf-runner-object-id> \
  --add-uamis \
  --uami-subscription <uami-subscription-id> \
  --uami-resource-group <uami-resource-group-name> \
  --uami-location <azure-region>
```

For example:

```sh
./setup-byo-app-registration.sh \
  --app-name cortex-scan-platform-my-subscription \
  --tf-runner-object-id 12345678-1234-1234-1234-123456789abc \
  --add-uamis \
  --uami-subscription 3ee44654-9e52-41a0-82ca-f5d5956452d6 \
  --uami-resource-group cortex-outpost-rg \
  --uami-location australiaeast
```

The script does everything the app-registration-only form does, and then:

* Creates the scanner UAMIs in your resource group.
* Grants the Terraform runner `Managed Identity Contributor` on that resource group.
* Grants the new app registration's service principal `Managed Identity Operator` on the same resource group. The second role grant is what allows Cortex's scanner dispatcher to attach your UAMIs to scanner VMs at scan time.

{% hint style="info" %}
**Note:** Adding scanner managed identities also activates the **Bring Your Own Scanner Managed Identities** toggle in the Cortex XSIAM wizard, which you will encounter when deploying the outpost.
{% endhint %}

#### Optional argument for scanner managed identities

When you create scanner managed identities, you can also pass an optional argument to customize the UAMI names.

| Argument                      | Default  | What it does                                                                                                          |
| ----------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `--uami-name-prefix <PREFIX>` | `cortex` | Sets the prefix for UAMI names. Each UAMI is named `<prefix>-<role>`, for example `cortex-agentless` or `myorg-dspm`. |

#### If the script fails

If any step fails, the script automatically rolls back everything it created in this run, so that you can fix the issue and rerun the script from a clean state.

For full details on flags, rollback behavior, manual rollback after a successful run, and troubleshooting, see:

* [Outpost troubleshooting](../../outpost-troubleshooting#bring-your-own-app-byoa-troubleshooting---azure).
* The `README.md` file that ships in the same directory as the script. The readme contains full details on flags, rollback behavior, manual rollback after a successful run, and additional troubleshooting.

### Shell script step 6: Copy the script output (terminal, editor)

When the script finishes, it prints a block of IDs to the terminal. In this step, you copy these IDs, which you will paste into the **Bring Your Own Scanner Managed Identities** section of the Cortex XSIAM outpost creation wizard when you deploy the outpost in the next task, [Task 3](#with-a-shell-script-recommended). Keep the terminal output open, or save the lines to a temporary file, until you complete the next task.

These IDs from the link between your new app registration (and UAMIs, if you created them) and the outpost.

<table><thead><tr><th width="275.6875">Returned ID</th><th width="277.5390625">Corresponding outpost creation wizard field</th><th width="141.1015625">When returned</th></tr></thead><tbody><tr><td><code>customer_app_client_id</code></td><td>Application (Client) ID</td><td>Yes</td></tr><tr><td><code>customer_sp_object_id</code></td><td>Service Principal Object ID</td><td>Yes</td></tr><tr><td><code>customer_uami_agentless_id</code></td><td>Agentless Disk Scanner Resource ID</td><td>Returned if you created scanner managed identities</td></tr><tr><td><code>customer_uami_dspm_id</code></td><td>DSPM Scanner Resource ID</td><td>Returned if you created scanner managed identities</td></tr><tr><td><code>customer_uami_registry_id</code></td><td>Registry Scanner Resource ID</td><td>Returned if you created scanner managed identities</td></tr><tr><td><code>customer_uami_serverless_id</code></td><td>Serverless Scanner Resource ID</td><td>Returned if you created scanner managed identities</td></tr><tr><td><code>customer_uami_proxy_id</code></td><td>Egress Proxy Resource ID</td><td>Returned if you created scanner managed identities</td></tr></tbody></table>

### What's next, after creating the app registration with the script?

Your app registration is ready to use, along with your scanner managed identities if you created them.

Proceed to [Task 3](../task-3-deploy-the-azure-byoa-outpost#step-1-create-the-azure-byoa-outpost-in-cortex) to map the IDs to, and deploy, the outpost.

## Manually in the Azure portal

This task is the manual alternative to the shell helper script approach, [Create app registration and scanner identities with a shell script](the-shell-script-for-azure-app-registration). You create the app registration, capture its identifiers, and add the Terraform runner as an owner by working through the Azure portal screens.

{% hint style="info" %}
**Note:** The shell script is the preferred path because it completes the same actions in a single command and prevents the most common deployment failures, but this manual procedure is available when you cannot or do not want to run the script.
{% endhint %}

The manual procedure creates only the app registration and its service principal. It does not create scanner managed identities (UAMIs). Later, when you [deploy the outpost](task-3-deploy-the-azure-byoa-outpost), Cortex creates the scanner managed identities for you.

{% hint style="info" %}
**Note:** To provide your own scanner managed identities, use the [shell script approach](the-shell-script-for-azure-app-registration) and add the `--add-uamis` flag instead of this manual task.
{% endhint %}

### Manual step 1: Before you begin

Confirm the prerequisites before you start. Skipping any of these causes the procedure to fail or causes a later `terraform apply` to fail.

* **Azure portal access:** A signed-in session for the Entra ID tenant where the app registration lives. This is usually your home tenant, not the monitored subscription's tenant.
* **Correct Entra ID tenant:** Before you open the portal, confirm which Entra ID tenant hosts the app registration. This is usually your home tenant, not the tenant that hosts the monitored subscription. If you sign in to the wrong tenant, you create the app registration in the wrong place, and the values you copy in [Step 3](#manual-step-3-copy-the-application-client-id-azure-portal) will not work with the Cortex XSIAM wizard.
* **Entra ID role:** Your account must hold the built-in `Application Developer` role on that tenant. By default any user can register applications, but if your tenant has disabled user registration, an administrator must grant you this role. Adding a service principal as an owner of the new app registration also requires the `Application Administrator` role on the tenant.
* **Terraform Runner Identity:** The service principal that runs `terraform apply` for this outpost must already exist in the same tenant. You add it as an owner of the new app registration in [Step 5](#manual-step-5-add-the-terraform-runner-as-an-owner-of-the-app-registration-azure-portal).

{% hint style="info" %}
**Note**: Third-party interfaces are subject to change. The screenshots provided in this topic might differ slightly from your current software version.
{% endhint %}

### Manual step 2. Create the app registration (Azure portal)

The app registration is the Entra ID identity that Cortex uses to authenticate into your monitored Azure subscription. You create it from the Microsoft Entra ID blade in the Azure portal.

{% hint style="info" %}
**Note:** Portal screens, field labels, and navigation paths reflect the cloud service provider's interface at the time of publication. Consult your cloud service provider's documentation for up-to-date instructions.
{% endhint %}

1. Sign in to the Azure portal.
2. Navigate to **Microsoft Entra ID** > **App registrations**. Confirm that the tenant selector in the top-right of the portal shows the correct Entra ID tenant. Click **+ New registration**.
3. Configure the new registration with the following values:
   * **Name:** Choose a unique display name for the app registration, for example `cortex-cloud-outpost-primary`.
   * **Supported account types:** Select **Accounts in any organizational directory (Any Microsoft Entra ID directory - Multitenant)**. Multi-tenant is required because the app registration consents into the monitored tenant, which may be different from the home tenant. Choosing single-tenant here causes the Terraform plan to fail later with a `sign_in_audience must be 'AzureADMultipleOrgs'` error.
   * **Redirect URI:** Leave this field blank. Cortex configures the redirect URI automatically during deployment.
4. Click **Register**.

### Manual step 3: Copy the application (client) ID (Azure portal)

The application (client) ID is the value that Cortex uses to identify your app registration. You provide it to the Cortex XSIAM wizard and to the Terraform variables file in the next subtask.

On the **Overview** page of your new app registration, locate the **Application (client) ID** value. Copy it and save it in a temporary location. This value is your `customer_app_client_id`.

### Manual step 4: Copy the service principal object ID (Azure portal)

The service principal object ID is a separate identifier from the application (client) ID. Both are GUIDs, both are returned by the Azure portal, and they are not interchangeable. Cortex needs both values in the next subtask.

On the **Overview** page of your app registration, in the **Essentials** section, click the **Managed application in local directory** link. The portal navigates to the **Enterprise application** view for the same identity.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2F7zRhzmEv7MTmTJJIIMNE%2Fapp-client-id.png?alt=media&#x26;token=133a72be-a157-4b59-b6d2-bb333bb35f6d" alt=""><figcaption></figcaption></figure>

On the **Properties** page of the enterprise application, locate the **Object ID** value.

Copy it and save it next to the application (client) ID. This value is your `customer_sp_object_id`.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FOHjqjJKxEPFzEyF5Op7q%2Fcustomer-sp-object.png?alt=media&#x26;token=04e309f4-657b-47ef-ac3c-964624a5b26c" alt=""><figcaption></figcaption></figure>

### Manual step 5: Add the Terraform runner as an owner of the app registration (Azure portal)

The Terraform runner needs to attach federated identity credentials to the app registration during `terraform apply`. Only owners of an app registration can attach federated identity credentials, so grant ownership now to avoid an HTTP 403 failure later.

Navigate back to **Microsoft Entra ID** > **App registrations**, and open your new app registration.

In the left navigation, select **Owners**, and then click **Add owners**.

In the search box, type the name or object ID of the Terraform Runner Identity. The service principal must be the same one that runs `terraform apply` for this outpost. Almost always this is a service principal, not a human user. If you select the wrong identity, the first federated identity credential creation fails at `terraform apply` time with an HTTP 403 / "Insufficient privileges" error.

Select the service principal in the search results, and click **Select**.

### Manual step 6: Record the values (editor)

In this step, you copy these IDs, which you will paste into the **Bring Your Own Scanner Managed Identities** section of the Cortex XSIAM outpost creation wizard when you deploy the outpost in the next task, Task 3. Keep the terminal output open, or save the lines to a temporary file, until you complete the next task.

These IDs from the link between your new app registration (and UAMIs, if you created them) and the outpost.

| ID                       | Where to find this value                                                                                                            | Where you use it next                                                           | Corresponding erraform variable (for reference only) |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Tenant                   | Available on the app registration **Overview** page as **Directory (tenant) ID**, or under **Microsoft Entra ID** > **Overview**.   | The **Tenant ID** field in the outpost creation wizard.                         |                                                      |
| App Client               | The **Application (client) ID** field on the app registration **Overview** page.                                                    | The **Application (Client) ID** field in the outpost creation wizard            | `customer_app_client_id`                             |
| Service Principal Object | The **Object ID** field on the enterprise application **Properties** page.                                                          | The **Service Principal Object ID** field in the outpost creation wizard        | `customer_sp_object_id`                              |
| Agentless Disk Scanner   | If you created scanner managed identities, navigate to **Managed Identities > \[**_**Your Agentless identity**_**] > Overview**.    | The **Agentless Disk Scanner Resource ID** field in the outpost creation wizard | `customer_uami_agentless_id`                         |
| DSPM Scanner             | If you created scanner managed identities, navigate to **Managed Identities > \[**_**Your DSPM identity**_**] > Overview**.         | The **DSPM Scanner Resource ID** field in the outpost creation wizard           | `customer_uami_dspm_id`                              |
| Registry Scanner         | If you created scanner managed identities, navigate to **Managed Identities > \[**_**Your Registry identity**_**] > Overview**.     | The **Registry Scanner Resource ID** field in the outpost creation wizard       | `customer_uami_registry_id`                          |
| Serverless Scanner       | If you created scanner managed identities, navigate to **Managed Identities > \[**_**Your Serverless identity**_**] > Overview**.   | The **Serverless Scanner Resource ID** field in the outpost creation wizard     | `customer_uami_serverless_id`                        |
| Egress Proxy             | If you created scanner managed identities, navigate to **Managed Identities > \[**_**Your Egress Proxy identity**_**] > Overview**. | The **Egress Proxy Resource ID** field in the outpost creation wizard           | `customer_uami_proxy_id`                             |

### What's next, after creating the app registration manually?

Your app registration is ready to use.

Continue to [Task 3](../task-3-deploy-the-azure-byoa-outpost#step-1-create-the-azure-byoa-outpost-in-cortex) to deploy the outpost by pasting the values from [Step 6](#step-6-record-the-values-editor) into the wizard and running `terraform apply` .
