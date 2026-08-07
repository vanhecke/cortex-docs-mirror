---
description: >-
  Learn how to execute the authentication template file in Microsoft Azure for
  subscriptions, tenants, and management groups. We provide instructions both
  for applying the Terraform template's configura
---

# Finalize Microsoft Azure onboarding by executing the authentication template

While onboarding Microsoft Azure with the onboarding wizard, you have to choose one of the following options for executing an authentication template: Download Terraform or Azure Resource Manager.

After running the wizard, you finalize the onboarding by executing the template to provision the resources for subscriptions, management groups, and tenants in your cloud environment.

After the template is successfully executed, the initial discovery scan starts. When the scan completes, view your cloud assets in Asset Inventory.

<details>

<summary>Finalize onboarding by applying the Terraform template's configuration</summary>

If you selected the **Download Terraform** option in the Microsoft Azure onboarding wizard, execute the template with the CLI. You decide, based on your own use case, how you would like to perform the CLI commands, for example, locally or in CloudShell.

{% hint style="info" %}
Prerequisites

Before you begin, ensure you have:

* An Azure subscription.
* A user with the required permissions for the relevant scope (subscription, management group, tenant). We recommend you create a dedicated role.
* Tenant ID and subscription ID. You can view these in Microsoft Azure Portal in **Management groups**.
* Installed Terraform on your local machine. You can download Terraform from the official [Terraform website](https://www.terraform.io/downloads.html) and follow the installation instructions for your operating system.
* Review the [Introduction to Terraform for Cloud service provider (CSP) onboarding](https://app.gitbook.com/s/mxWuY3s7AUvWfzCV9p1A/deployment-steps-and-checklist/cloud-service-provider-csp-onboarding/introduction-to-terraform-for-cloud-service-provider-csp-onboarding) to get familiar with how Cortex works with Terraform for cloud onboarding.
* Installed the [Azure CLI tool](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).
{% endhint %}

1. In your local terminal, log in to your Azure account using the Azure CLI:

`az login`

2. Create a directory on your local machine to store and run the Terraform code. If you have more than one Azure connector, you need a separate directory for each one:

`mkdir -p ~/terraform/azure-connector-1`

3. Navigate to the directory you created and extract the Terraform files. Ensure all necessary Terraform files are present (main.tf, template\_params.tfvars, and so on).

Do not delete or move the Terraform files from this folder. It will prevent you from being able to edit your cloud instance in the future.

```
cd ~/terraform/azure-connector-1
tar -xzvf <your_template>.tar.gz.
```

4. Initialize Terraform in your project directory:

`terraform init`

5. Apply your Terraform configuration using the downloaded parameter file:

`terraform apply --var-file=template_params.tfvars`

* When the CLI prompts you for a Group ID, enter the management group ID or the root tenant ID where you want to create Cortex XSIAM resources.
* When the CLI prompts you for a Subscription ID, enter the subscription ID where you want to create Cortex XSIAM resources. (This subscription is typically a subscription that the security team manages.)

6. When prompted, review the actions the Terraform will perform and approve them by entering yes.

The Terraform template is executed.

</details>

<details>

<summary>Finalize onboarding of subscriptions by deploying the Microsoft Azure Resource Manager (ARM) template</summary>

If you selected the **Azure Resource Manager** option in the Microsoft Azure onboarding wizard to onboard subscriptions, deploy the template with the CLI. You decide, based on your use case, how you would like to perform the CLI commands, for example, locally or in CloudShell.

{% hint style="info" %}
Prerequisites

Before you begin, ensure you have:

* An Azure subscription.
* A user with the required permissions for the relevant scope (subscription, management group, tenant). We recommend you create a dedicated role.
* Tenant ID and subscription ID. You can view these in Microsoft Azure Portal in **Management groups**.
* Installed the [Azure CLI tool](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).
* Authorization to create management group policies.
{% endhint %}

1. In your local terminal or CloudShell, log in to your Azure account using the Azure CLI:

`az login`

2. Deploy the template file.

```
az deployment sub create \
   --location <LOCATION> \
   --subscription <SUBSCRIPTION_ID> \
   --template-file <JSON_TEMPLATE> 
```

where:

* \<LOCATION> is the location of the management group, such as eastus or westus.
* \<SUBSCRIPTION\_ID> is the ID of the subscription you want to onboard.
* \<JSON\_TEMPLATE> is the JSON template file that you downloaded at the end of the onboarding wizard.

To verify the deployment was successful, check the Azure Portal under the "Deployments" section of the targeted subscription.

</details>

<details>

<summary>Finalize onboarding of tenants and management groups by deploying the Microsoft Azure Resource Manager (ARM) template</summary>

If you selected the Azure Resource Manager option in the Microsoft Azure onboarding wizard to onboard tenants or management groups, deploy the template with the CLI using Bash in CloudShell.

{% hint style="info" %}
Prerequisites

Before you begin, ensure you have:

* An Azure subscription.
* A user with the required permissions for the relevant scope (subscription, management group, tenant). We recommend you create a dedicated role.
* Tenant ID and subscription ID. You can view these in Microsoft Azure Portal in **Management groups**.
* Installed the [Azure CLI tool](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).
* Authorization to create management group policies.
{% endhint %}

1. To prepare for deployment, execute the following commands in a Bash-compliant terminal, such as the Bash environment in Azure Cloud Shell:
   1. | Step                                                                                                                                                  | Command                                                    |
      | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
      | Create a folder on your local machine to store the `tar` file. If you have more than one Azure connector, you need a separate directory for each one. | `mkdir -p ~/azure-connector-1`                             |
      | Navigate to the directory you created and extract the files.                                                                                          | `cd ~/azure-connector-1 tar -xzvf <your_template>.tar.gz.` |
2.  Deploy the template file: `bash onboard.sh`

    When prompted, enter the following values:

    * The Azure region where you want the resources to be created, such as `eastus` or `westus`.
    * The ID of the management group or tenant that you want to onboard.
    * The ID of the subscription where the deployment script will run.

    To verify the deployment was successful, check the Azure Portal under the **Deployments** section of the targeted management group, or tenant.

</details>
