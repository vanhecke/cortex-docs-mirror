---
description: >-
  How to offboard a Microsoft Azure tenant onboarded with the Entra ID only
  option from Cortex XSIAM: A step-by-step technical guide to safely removing
  deployed resources.
---

# Offboard Azure tenant with Entra ID only

Follow this procedure to offboard a Microsoft Azure tenant that was onboarded with the Entra ID-only option and cleanly decommission all deployed resources.

{% hint style="warning" %}
#### Important

This offboarding script is designed for environments onboarded with BASE template version 1.0.10 or later. If your onboarding was deployed with an older BASE template version, this script may not fully remove all provisioned resources and could leave orphaned artifacts. Please verify your onboarding template version before proceeding.
{% endhint %}

### Prerequisites

Before you begin, ensure you meet the following requirements:

#### Tooling Requirements

* Bash (version $$\ge$$ 4.0)
* Azure CLI (version $$\ge$$ 2.61)
* jq (JSON processor)

#### Working directory

You must run the offboarding script from the same directory where the files `parameters.sh` and `graphAPIRoles.json` are located. These files are packaged with the onboarding template:

* `parameters.sh`: Contains configuration parameters (such as `resource_suffix`, `tenant_id`, and `customer_object_id`) which the script auto-loads at startup.
* `graphAPIRoles.json`: Defines the Microsoft Graph app role assignments to remove.

#### Required Azure permissions

The authenticated session must be run by a user or service principal with the following roles:

* **Global Administrator:** Required for managing Entra ID diagnostic settings and service principal operations.
* **Owner:** Required at the management group scope for deleting deployment stacks, role assignments, role definitions, and resource groups.

#### Authentication

Run the following command in your terminal to authenticate with the correct Azure tenant:

```bash
az login --tenant <tenant-id>
```

## How to offboard Microsoft Azure with Entra ID only

{% stepper %}
{% step %}
### Make the script executable

Set the execution permissions for the script within your working directory. In your local terminal within the directory containing your onboarding templates and configuration files, run:

```bash
chmod +x offboard_entra_id_only.sh
```
{% endstep %}

{% step %}
### Run the `offboard_entra_id_only.sh` script

Run the offboarding script to clean up all deployed infrastructure. For your reference, the following flags are used in the script:

<table data-header-hidden><thead><tr><th width="279.1171875"></th><th></th></tr></thead><tbody><tr><td><strong>Flag</strong></td><td><strong>Description</strong></td></tr><tr><td><code>--management-group-id &#x3C;mg-id></code></td><td><strong>Required</strong>. Management group ID. Typically this is the tenant-root MG.</td></tr><tr><td><code>--subscription-id &#x3C;sub-id></code></td><td><strong>Required</strong>. The specific subscription hosting the onboarding resource group.</td></tr><tr><td><code>--resource-suffix &#x3C;rs></code></td><td>The resource suffix from onboarding. This is automatically loaded from <code>./parameters.sh</code> if present in the working directory.</td></tr><tr><td><code>--no-dry-run</code></td><td>Action Flag. By default, the script runs in dry-run (read-only) mode. You must pass this flag to perform actual resource deletions.</td></tr><tr><td><code>--yes</code> or <code>-y</code></td><td>Automation Flag. Skips the interactive confirmation prompt before a destructive run.</td></tr><tr><td><code>--ext-resource-suffix &#x3C;ext></code></td><td>Override Flag. Overrides the automatic resolution of the <code>extResourceSuffix</code>. Required if the deployment stack has already been deleted and auto-resolution fails.</td></tr></tbody></table>

1.  First run a dry-run to preview the planned deletions and ensure your permissions are correct:

    ```bash
    ./offboard_entra_id_only.sh \
      --management-group-id <mg-id> \
      --subscription-id <sub-id>
    ```
2.  After reviewing the dry-run output, run the script with `--no-dry-run` to delete the resources:

    ```bash
    ./offboard_entra_id_only.sh \
      --management-group-id <mg-id> \
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

<details>

<summary>Reference: Script exit codes</summary>

Use the following exit codes to understand the script results:

<table data-header-hidden><thead><tr><th width="115.796875"></th><th></th></tr></thead><tbody><tr><td><strong>Exit Code</strong></td><td><strong>Meaning</strong></td></tr><tr><td><code>0</code></td><td>Success: Dry-run completed, or resources successfully deleted.</td></tr><tr><td><code>10</code></td><td>Preflight failure: Missing flags, authentication error, or <code>extResourceSuffix</code> unresolvable (pass <code>--ext-resource-suffix</code>).</td></tr><tr><td><code>21</code></td><td>Phase 1 (diagnostics) failure.</td></tr><tr><td><code>22</code></td><td>Phase 2 (stack) failure.</td></tr><tr><td><code>23</code></td><td>Phase 3 (onboarding RG) failure. <em>(Note: Deletion is automatically skipped if a managed identity is found inside the Resource Group, indicating it is shared with a full tenant onboarding).</em></td></tr><tr><td><code>24</code></td><td>Phase 4 (graph-api-roles) failure.</td></tr><tr><td><code>30</code></td><td>Phase 5 (verify) failure: Leftover resources were detected.</td></tr><tr><td><code>40</code></td><td>Multiple failures: Two or more deletion phases failed.</td></tr><tr><td><code>130</code></td><td>Execution interrupted (SIGINT).</td></tr></tbody></table>

</details>
