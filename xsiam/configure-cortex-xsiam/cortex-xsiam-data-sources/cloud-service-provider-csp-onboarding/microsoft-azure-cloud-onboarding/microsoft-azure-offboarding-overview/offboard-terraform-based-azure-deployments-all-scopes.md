---
description: >-
  How to offboard all Terraform-based Microsoft Azure scopes from Cortex XSIAM:
  A step-by-step technical guide to safely running Terraform destroy and
  cleaning up policy-deployed resources.
---

# Offboard Terraform-based Azure deployments (all scopes)

Follow this procedure to offboard all Terraform-based Microsoft Azure scopes (subscription, management group, or tenant) and cleanly decommission all Cortex XSIAM resources from Microsoft Azure. Fo

### Prerequisites

Before you begin, ensure you meet the following requirements:

#### Tooling requirements

* Bash (version $$\ge$$ 4.0)
* Azure CLI (version $$\ge$$ 2.61)
* jq (JSON processor)
* Terraform CLI (initialized in your Cortex deployment directory)

#### Required Azure permissions

The authenticated session must be run by a user or service principal with the **Owner** role assigned at the management group scope. This is required to delete policy resources, role assignments, role definitions, and resource groups across all child subscriptions.

#### Authentication

Run the following command in your terminal to authenticate with the correct Azure tenant:

```bash
az login --tenant <tenant-id>
```

## How to offboard Microsoft Azure

{% tabs %}
{% tab title="Azure subscription scope" %}
1.  In the same Terraform directory used to deploy, run the destruction command. This removes all core Terraform-managed resources, including the deployment stack, onboarding resource group, managed identity, and diagnostic settings:

    ```bash
    terraform destroy
    ```
2. Review the destruction plan carefully, then enter `yes` to confirm the removal.
{% endtab %}

{% tab title="Azure MG or tenant scope" %}
### 1. Identify `ext_resource_suffix`

{% hint style="warning" %}
#### Important

This step must be performed before destroying any resources. Once `terraform destroy` is executed, the Terraform state is cleared, and this value cannot be recovered without contacting Palo Alto Networks support.
{% endhint %}

1.  In your local terminal within the directory containing your Cortex XSIAM Terraform configuration and run the following command to retrieve the unique resource suffix:

    ```bash
    terraform output ext_resource_suffix
    ```
2. Copy and save the output string. It is referred to as `<ext-value>` in the steps below.

### 2. Run `terraform destory`

This removes all core Terraform-managed resources, including the deployment stack, onboarding resource group, managed identity, diagnostic settings, and Graph API roles.

1.  In the same Terraform directory used in Step 1, run the destruction command:

    ```bash
    terraform destroy
    ```
2. Review the destruction plan carefully, then enter `yes` to confirm the removal.

### 3. Run `offboard_policy_deployment.sh`

Certain policy-deployed resources are created per-subscription by a `deployIfNotExists` policy and exist outside the Terraform lifecycle, so `terraform destroy` cannot remove them. The `offboard_policy_deployment.sh` script must be executed to finalize the offboarding.

For your reference, the following flags are used in the script:

<table data-header-hidden><thead><tr><th width="307.4921875"></th><th></th></tr></thead><tbody><tr><td><strong>Flag</strong></td><td><strong>Description</strong></td></tr><tr><td><code>--management-group-id &#x3C;id></code></td><td><p><strong>Required</strong>. Scope-specific values for <code>--management-group-id</code>:</p><ul><li><strong>Subscription scope</strong>: Pass the management group ID that contains the subscription being offboarded.</li><li><strong>Management group scope</strong>: Pass the specific management group ID being offboarded.</li><li><strong>Tenant scope</strong>: Pass the tenant-root management group ID.</li></ul></td></tr><tr><td><code>--ext-resource-suffix &#x3C;ext-value></code></td><td><strong>Required</strong>. The suffix value saved from Step 1.</td></tr><tr><td><code>--no-dry-run</code></td><td>Action Flag. By default, the script runs in read-only mode. You must pass this flag to execute actual resource deletions.</td></tr><tr><td><code>--yes</code> or <code>-y</code></td><td>Automation Flag. Skips the interactive confirmation prompt. (Required for CI/CD pipelines, ignored in dry-run mode).</td></tr></tbody></table>

1.  First run a dry-run to preview the planned deletions and ensure your permissions are correct:

    ```bash
    bash offboard_policy_deployment.sh \
      --management-group-id <mg-id> \
      --ext-resource-suffix <ext-value>
    ```
2. Review the script output and confirm that all targeted resources were removed. The script runs a post-deletion verification phase automatically. A final summary is printed to the terminal indicating the outcome of each phase.\
   If the script exits with a non-zero code or reports leftover resources in the verification phase, it is usually due to transient Azure API delays. You can safely re-run the script with `--no-dry-run` to trigger another cleanup and verification sweep.
3.  After reviewing the dry-run output, run the script with `--no-dry-run` to delete the resources:

    ```bash
    bash offboard_policy_deployment.sh \
      --management-group-id <mg-id> \
      --ext-resource-suffix <ext-value> \
      --no-dry-run
    ```
{% endtab %}
{% endtabs %}
