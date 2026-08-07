---
description: >-
  How to offboard Microsoft Azure management group or tenant scopes from Cortex
  XSIAM: A step-by-step technical guide to safely removing all Azure resources
  deployed by Cortex onboarding templates.
---

# Offboard Azure management group or tenant scope (ARM)

Follow this procedure to offboard a Microsoft Azure Management Group or Tenant scope from Cortex XSIAM and cleanly decommission all deployed resources.

{% hint style="warning" %}
#### Important

This offboarding script is designed for environments onboarded with BASE template version 1.4.18 or later. If your onboarding was deployed with an older BASE template version, this script may not fully remove all provisioned resources and could leave orphaned artifacts. Please verify your onboarding template version before proceeding.
{% endhint %}

### Prerequisites

Before you begin, ensure you meet the following requirements:

#### Tooling requirements

* Bash (version $$\ge$$ 4.0)
* Azure CLI (version $$\ge$$ 2.61)
* jq (JSON processor)

#### Working directory

You must run the offboarding script from the same directory where the files `parameters.sh` and `graphAPIRoles.json` are located. These files are packaged with the onboarding template:

* `parameters.sh`: Contains configuration parameters (such as `resource_suffix`, `tenant_id`, and `customer_object_id`) which the script auto-loads at startup.
* `graphAPIRoles.json`: Defines the Microsoft Graph app role assignments to remove.

#### Required Azure permissions

The authenticated session must be run by a user or service principal with the following roles:

* Global Administrator: Required for managing Entra ID diagnostic settings and service principal operations.
* Owner: Required at the management group scope for deleting deployment stacks, policy resources, role assignments, role definitions, and resource groups.

#### Authentication

Run the following command in your terminal to authenticate with the correct Azure tenant:

```bash
az login --tenant <tenant-id>
```

## How to offboard Microsoft Azure MG or tenant scope - ARM method

{% stepper %}
{% step %}
### Gather required values

Before running the offboarding script, collect the following values:

<table><thead><tr><th width="143.01953125">Variable</th><th>Description</th><th>Where to find it</th></tr></thead><tbody><tr><td><code>&#x3C;mg-id></code></td><td>The management group ID being offboarded.</td><td><strong>Azure portal > Management groups</strong>, or run <code>az account management-group list -o table</code>.</td></tr><tr><td><code>&#x3C;tenant-root-mg-id></code></td><td>The tenant-root management group ID (for tenant scope only). Typically matches your Azure tenant ID.</td><td><strong>Azure portal > Management groups > the top-level group</strong>, or run <code>az account management-group list -o table</code>.</td></tr><tr><td><code>&#x3C;sub-id></code></td><td>The subscription ID hosting the Cortex onboarding resource group (<code>cortex-onboarding-&#x3C;resource_suffix></code>).</td><td><strong>Azure portal > Subscriptions</strong>, or run <code>az account list -o table</code>.</td></tr></tbody></table>
{% endstep %}

{% step %}
### Locate your offboarding bundle

Navigate to the directory containing these files before proceeding. The bundle contains the following files, which must all be present in the same directory:

<table><thead><tr><th width="215.546875">File</th><th>Description</th></tr></thead><tbody><tr><td><code>parameters.sh</code></td><td>Connector-specific parameters, including <code>resource_suffix</code>, <code>tenant_id</code>, and <code>customer_object_id</code>. Auto-loaded by the script at startup.</td></tr><tr><td><code>graphAPIRoles.json</code></td><td>Defines which Microsoft Graph app role assignments to remove.</td></tr><tr><td><code>offboard_mg_tenant.sh</code></td><td>Interactive offboarding script.</td></tr></tbody></table>
{% endstep %}

{% step %}
### Understand the offboarding phases

The script executes the following phases in a fixed order. In dry-run mode, each phase lists the resources it would delete without making any changes. In action mode, each phase deletes the identified resources and the final phase verifies that all resources have been removed.

<table><thead><tr><th width="135.52734375">Script phase</th><th>What it does</th></tr></thead><tbody><tr><td><code>diagnostics</code></td><td>Deletes the management group diagnostic setting. For tenant scope, also deletes the Entra ID diagnostic setting.</td></tr><tr><td><code>stack</code></td><td>Deletes the deployment stack <code>cortex-policy-&#x3C;resource_suffix></code> at management group scope.</td></tr><tr><td><code>onboarding-rg</code></td><td>Deletes the onboarding resource group <code>cortex-onboarding-&#x3C;resource_suffix></code>, which cascades deletion of the managed identity.</td></tr><tr><td><code>graph-api-roles</code></td><td>Removes Microsoft Graph app role assignments from the customer service principal.</td></tr><tr><td><code>policy</code></td><td>Deletes per-subscription policy-deployed resources across all child subscriptions: role assignments, role definitions, and the policy resource group.</td></tr><tr><td><code>verify</code></td><td>Confirms all targeted resources are gone. Skipped in dry-run mode.</td></tr></tbody></table>
{% endstep %}

{% step %}
### Run the `offboard_mg_tenant.sh` script in dry-run mode

First, run the script in dry-run mode (the default) to preview all resources that would be deleted and verify your permissions are correct. No changes are made during a dry run.

For management group scope, run:

```shellscript
 bash offboard_mg_tenant.sh \
  --scope management_group \
  --management-group-id <mg-id> \
  --subscription-id <sub-id>
```

For tenant scope run:

```shellscript
bash offboard_mg_tenant.sh \
  --scope tenant \
  --management-group-id <tenant-root-mg-id> \
  --subscription-id <sub-id>
```

Review the dry-run output carefully and confirm that the listed resources are correct before proceeding.
{% endstep %}

{% step %}
### Run the offboarding cleanup

After reviewing the dry-run output, run the script with `--no-dry-run` to delete the resources.

For a **management group** scope connector:

```bash
bash offboard_mg_tenant.sh \
  --scope management_group \
  --management-group-id <mg-id> \
  --subscription-id <sub-id> \
  --no-dry-run
```

For a **tenant** scope connector:

```bash
bash offboard_mg_tenant.sh \
  --scope tenant \
  --management-group-id <tenant-root-mg-id> \
  --subscription-id <sub-id> \
  --no-dry-run
```
{% endstep %}

{% step %}
### Verification and troubleshooting

Review the script output and confirm that all targeted resources were removed:

* **Success:** You will see a final confirmation message in your terminal indicating that cleanup is complete (Exit Code `0`).
* **Leftover Resources:** If the script times out or detects that any policy-deployed resources still remain, it will log the specific failed resources in the console output and exit with code `30`. This is usually due to transient Azure API replication delays. You can safely re-run the cleanup script with the `--no-dry-run` flag to trigger another verification and cleanup sweep. See [#reference-script-exit-codes](#reference-script-exit-codes "mention") for the exit code details.
{% endstep %}
{% endstepper %}

### Troubleshooting

**The deployment stack was already deleted**

If the deployment stack was deleted manually or in a prior partial run, the script cannot auto-resolve the `extResourceSuffix` and exits with code `10`. The value of `<ext-value>` is printed in the logs when you run the offboard script. Pass the `--ext-resource-suffix` flag with that value to resume:

```bash
bash offboard_mg_tenant.sh \
  --scope <tenant|management_group> \
  --management-group-id <mg-id> \
  --subscription-id <sub-id> \
  --ext-resource-suffix <ext-value> \
  --no-dry-run
```

**Verification fails after the action**

The script automatically re-runs the cleanup and re-verifies up to three times. Transient Azure API delays are the most common cause. If issues persist after three attempts, inspect the remaining resources using the IDs shown in the verification output and re-run the script with `--no-dry-run` to trigger another cleanup sweep.

<details>

<summary>Reference: Script exit codes</summary>

Use the following exit codes to understand the script results:

<table><thead><tr><th width="88.29296875">Code</th><th>Meaning</th></tr></thead><tbody><tr><td><code>0</code></td><td>Success, dry-run completed, or nothing to delete</td></tr><tr><td><code>10</code></td><td>Preflight failure (missing flag, authentication error, or <code>extResourceSuffix</code> unresolvable. Pass <code>--ext-resource-suffix</code>)</td></tr><tr><td><code>21–25</code></td><td>Single phase failure (diagnostics / stack / onboarding-rg / graph-api-roles / policy)</td></tr><tr><td><code>30</code></td><td>Verification found leftover resources</td></tr><tr><td><code>40</code></td><td>Two or more phases failed</td></tr><tr><td><code>130</code></td><td>Interrupted (SIGINT)</td></tr></tbody></table>

</details>
