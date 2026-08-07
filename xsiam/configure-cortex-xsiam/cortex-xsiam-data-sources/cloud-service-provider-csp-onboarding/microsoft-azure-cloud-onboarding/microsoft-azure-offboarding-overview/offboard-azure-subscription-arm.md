---
description: >-
  How to offboard a Microsoft Azure subscription scope that was onboarded using
  ARM: A step-by-step technical guide to safely running the interactive
  offboarding script and cleaning up all resources.
---

# Offboard Azure subscription (ARM)

Follow this procedure to offboard a Microsoft Azure subscription scope from Cortex XSIAM and cleanly decommission all Cortex XSIAM resources from Microsoft Azure. This method is only for cloud instances that were onboarded using the Azure Resource Manager (ARM) method.

### Prerequisites

Before you begin, ensure you meet the following requirements.

#### Tooling requirements <a href="#tooling-requirements" id="tooling-requirements"></a>

* Azure CLI (version ≥ 2.61)
* jq (JSON processor)
* Bash (version ≥ 4.0)

#### Required Azure permissions <a href="#required-azure-permissions" id="required-azure-permissions"></a>

The authenticated session must be run by a user or service principal with the **Owner** role assigned at the subscription scope. This is required to delete role assignments, role definitions, diagnostic settings, and the Cortex resource group.

#### Authentication

Run the following command in your terminal to authenticate:

```
az login
```

## How to offboard an Azure subscription scope - ARM method

{% stepper %}
{% step %}
### Locate your offboarding bundle

Locate the offboarding bundle provided by Cortex XSIAM. Navigate to the directory containing these files before proceeding. The bundle contains the following files, which must all be present in the same directory:

<table><thead><tr><th width="282.890625">File</th><th>Description</th></tr></thead><tbody><tr><td><code>connectors_azure_arm-&#x3C;id>.json</code></td><td>The original ARM deployment template used during onboarding</td></tr><tr><td><code>parameters.sh</code></td><td>Connector-specific parameters, including <code>resource_suffix</code></td></tr><tr><td><code>offboard_subscription_arm.sh</code></td><td>Interactive offboarding script</td></tr></tbody></table>
{% endstep %}

{% step %}
### Run the offboarding script

{% hint style="warning" %}
#### Important

The script must be run from the directory containing `parameters.sh`. Running it from any other directory will cause it to exit with an error.
{% endhint %}

Execute the offboarding script:

```bash
bash offboard_subscription_arm.sh
```

The script is interactive and guides you through each step. When prompted, provide the following inputs:

1. Subscription ID: Enter the Azure subscription ID to offboard, or press **Enter** to use the currently active subscription.
2. Execution mode: Select one of the following:
   * `[1] plan` — Dry run. Lists all role definitions, role assignments, diagnostic settings, and the resource group that would be deleted, along with their current status in Azure. No changes are made. After the plan is shown, you are offered the option to proceed with the action.
   * `[2] action` — Executes the cleanup immediately, deleting all identified resources.
{% endstep %}

{% step %}
### Review the plan output

If you selected plan mode, review the output carefully. Each resource is listed with one of the following statuses:

* `EXISTS`: The resource is present in Azure and will be deleted when you run the action.
* `DOESN'T EXIST`: The resource has already been removed.

If all resources show `DOESN'T EXIST`, the subscription has already been fully offboarded. The script will offer to delete the ARM deployment records and exit.

If any resources show `EXISTS`, confirm the plan and enter `y` when prompted to proceed with the action.
{% endstep %}

{% step %}
### Confirm resource deletion

When the action runs, the script deletes the following resources in order:

* Custom role assignments created by the ARM template
* Custom role definitions created by the ARM template
* Diagnostic settings created by the template
* The Cortex resource group (`cortex-<resource_suffix>`)

Review the script output and confirm that all targeted resources are removed.
{% endstep %}

{% step %}
### Verification

After the action completes, the script automatically waits 10 seconds and then runs a verification check to confirm that all resources have been deleted. This verification runs up to three times. If any resources are still detected on a given attempt, the script re-runs the cleanup before verifying again.

You will see one of the following final messages:

* `Verification passed. Offboarding complete.` : This means that all resources have been successfully removed.
* `❌ Verification failed after 3 attempt(s). N issue(s) remain.`: This means that some resources could not be deleted. Inspect the specific resource IDs shown in the verification output and re-run the script manually.

If verification passes, the script prompts you to optionally delete the ARM deployment records from Azure. Enter `y` to remove them or `N` to retain them.
{% endstep %}
{% endstepper %}

### Troubleshooting

**No resource group found, but a failed deployment exists**

If the Cortex resource group is not found, the script checks for a failed ARM deployment. If a failed deployment is detected, it identifies any orphaned role definitions and role assignments that were created before the failure, shows a plan of what would be deleted, and prompts you to confirm cleanup. After cleanup, you are offered the option to delete the failed deployment record.

**Verification fails after the action**

The script automatically re-runs the cleanup and re-verifies up to three times. Transient Azure API delays are the most common cause. If issues persist after three attempts, inspect the remaining resources using the IDs shown in the verification output and re-run the script with mode `[2] action` to trigger another cleanup sweep.
