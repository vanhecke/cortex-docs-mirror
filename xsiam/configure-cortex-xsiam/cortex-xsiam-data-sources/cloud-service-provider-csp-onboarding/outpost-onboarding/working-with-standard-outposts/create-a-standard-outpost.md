---
description: Instructions for creating a standard outpost while onboarding your CSP.
---

# Create a standard outpost

{% hint style="info" %}
**License type**: This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM product that has the Cloud Runtime Security add-on.
{% endhint %}

Create an outpost to deploy a Cortex XSIAM outpost using infrastructure that Cortex XSIAM creates for a fast, consistent deployment with minimal manual configuration.

## Step 1. Plan and prepare

Review the [fundamentals and prerequisites](../../outpost-fundamentals-and-planning#outpost-planning) before starting.

{% hint style="info" %}
**Notes:**

* Before you create your outpost, verify that your internet connection is active. An active internet connection is necessary for the notification to be sent to Cortex XSIAM to create the new outpost.
* (Azure) Due to limitations in Terraform, the Azure subscription name cannot contain blanks. Take this into account while onboarding.
{% endhint %}

## Step 2. Define the outpost with the outpost creation wizard

Start the outpost creation wizard:

1. In Cortex XSIAM, navigate to **Settings → Data Sources & Integrations → Outposts**.
2. Click **New Outpost**.

{% hint style="info" %}
**Tip**: Alternatively, while onboarding your Cortex XSIAM with the cloud service provider (CSP) onboarding wizard, the wizard prompts you to choose a scan mode: Cloud scan or Outpost scan. When choosing Outpost scan, you have the opportunity to create your outpost. To start the cloud service provider (CSP) onboarding wizard, navigate to **Settings → Data Sources & Integrations → Add New**.
{% endhint %}

Perform the steps according to your CSP.

<details>

<summary>AWS</summary>

1. Choose **AWS**.
2. If you are using a FedRAMP-certified (Government) Cortex XSIAM tenant, you are able to choose between the following environments:
   * **Commercial:** (Default) Standard cloud deployment typically used for private and public sector organizations that do not require isolated government-specific infrastructure.
   * **Government:** AWS GovCloud environments for compatibility with FedRAMP-certified tenants.
3. Enter the AWS account instance name.
4. (Optional) Define tags and tag values to be added to any new resource created by Cortex in the cloud environment. Click **Next**.
5. Click **Download Terraform** to download the Terraform template file.

</details>

<details>

<summary>Azure</summary>

When creating an outpost for a specific Azure subscription, the outpost account must be in the same Azure organization as the monitored subscriptions.

{% hint style="info" %}
**Important**: If you want to deploy a Cortex XSIAM Azure outpost using your own pre-created Entra ID app registration, follow the instructions for [Bringing your own Azure app (BYOA)](../working-with-bringing-your-own-azure-app-byoa-outposts). This type of outpost is designed for organizations with strict governance policies that require control over Entra ID tenant-level resources.
{% endhint %}

1. Choose **Azure.**
2. If you are using a FedRAMP-certified (Government) Cortex XSIAM tenant, you are able to choose between the following environments:
   * **Commercial:** (Default) Standard cloud deployment typically used for private and public sector organizations that do not require isolated government-specific infrastructure.
   * **Government:** Microsoft Azure Government environments for compatibility with FedRAMP-certified tenants.
3. Enter the instance name and the tenant ID of the Azure tenant in which you want to establish the outpost.\
   \
   **Note**: Due to limitations in Terraform, the Azure subscription name cannot contain blanks.
4. (Optional) Define tags and tag values to be added to any new resource created by Cortex in the cloud environment. Click **Next**.
5. If you are deploying the outpost with your own pre-created Entra ID app registration:
   1. Click **Show advanced settings** and toggle **Bring Your Own App (BYOA)** on.
   2. Skip to the instructions for [bringing your own Azure app (BYOA)](../working-with-bringing-your-own-azure-app-byoa-outposts), without performing the steps here.
6. Click **Download Terraform** to download the Terraform template file.

</details>

<details>

<summary>GCP</summary>

1. Choose **GCP**.
2. If you are using a FedRAMP-certified (Government) Cortex XSIAM tenant, you are able to choose between the following environments:
   * **Commercial:** (Default) Standard cloud deployment typically used for private and public sector organizations that do not require isolated government-specific infrastructure.
   * **Government:** GCP Assured Workloads for compatibility with FedRAMP-certified tenants.
3. Enter the project ID of the GCP project.
4. (Optional) Define tags and tag values to be added to any new resource created by Cortex in the cloud environment. Click **Next**.
5. Click **Download Terraform** to download the Terraform template file.

</details>

## Step 3. **Execute the template in the CSP to deploy the outpost**

In the previous step, you downloaded the Terraform template file in the outpost creation wizard.

Now, you log in to your CSP and execute the Terraform template file.

Perform the steps according to your CSP.

<details>

<summary>AWS</summary>

1. **Prerequisites:** Before you begin, ensure you have:
   * An AWS account.
   * Permission to create a stack and its resources in AWS.
   * Installed Terraform on your local machine. You can download Terraform from the official Terraform website and follow the installation instructions for your operating system.
   * Installed the AWS CLI tool and configured your profile with the `aws configure sso` wizard.
2. Open your local terminal (Command prompt, PowerShell, or Terminal).
3.  Log in to your AWS account using the AWS CLI:

    ```
    aws sso login --profile <my-profile>
    ```

    `<my-profile>` is the profile you configured with the `aws configure sso` wizard.
4.  Create a directory on your local machine to store and run the Terraform code. If you are creating more than one outpost, you need a separate directory for each one:

    ```
    mkdir -p ~/terraform/aws-outpost-1
    ```
5.  Navigate to the directory you created and extract the Terraform files.

    ```
    cd ~/terraform/aws-outpost-1
    tar -xzvf <your_template>.tar.gz
    ```
6.  Initialize Terraform in your project directory:

    ```
    terraform init
    ```
7.  Apply your Terraform configuration using the downloaded parameter file. When prompted, enter the subscription ID:

    ```
    terraform apply --var-file=template_params.tfvars
    ```
8. When prompted, review the actions Terraform will perform and approve them by entering **yes**.

The Terraform template is deployed, and your outpost is created in pending status.

To view all outposts and their details, navigate to **Settings → Data Data Sources & Integrations → Outposts**.

</details>

<details>

<summary>Azure</summary>

> **Important**: If you are deploying the outpost with your own pre-created Entra ID app registration, and you are ready to execute the template in Azure, skip to the instructions for [deploying your own Azure app (BYOA)](../../working-with-bringing-your-own-azure-app-byoa-outposts/task-3-deploy-the-azure-byoa-outpost#step-2-execute-the-template-in-azure-to-deploy-the-outpost), without performing the steps here.

1. **Prerequisites:** Before you begin, ensure you have:
   * An active Azure subscription.
   * Installed the Azure CLI tool.
   * Permission to deploy a custom template and create its resources in Microsoft Azure ("Owner" or "Contributor" on the designated outpost subscription scope, and Active Directory "Cloud Application Administrator" or "Application Administrator" privileged roles).
   * Installed Terraform 1.9.4 or above on your local machine. You can download Terraform from the official Terraform website and follow the installation instructions for your operating system.
   * A static egress IP assigned to the machine running this Terraform. This is used to configure the Azure Storage IP whitelist (Recommended). Without this, future runs of this Terraform may fail on Azure storage configurations.
2. Open your local terminal (Command Prompt, PowerShell, or Terminal).
3.  Log in to your Azure account using the Azure CLI:

    ```
    az login
    ```
4.  If prompted, select the subscription\_id of the designated subscription, or run:

    ```
    az account set --subscription <subscription_id>
    ```

    Where `<subscription_id>` is the subscription ID of the designated subscription.
5.  Create a directory on your local machine to store and run the Terraform code. If you are creating more than one outpost, you need a separate directory for each one:

    ```
    mkdir -p ~/terraform/azure-outpost-1
    ```
6.  Navigate to the directory you created and extract the Terraform files.

    ```
    cd ~/terraform/azure-outpost-1
    tar -xzvf <your_template>.tar.gz
    ```
7.  Initialize Terraform in your project directory:

    ```
    terraform init
    ```
8.  Apply your Terraform configuration using the downloaded parameter file. When prompted, enter the subscription ID:

    ```
    terraform apply --var-file=template_params.tfvars
    ```
9. When prompted for `var.storaage_account_ip_whitelist`, you can leave it empty to enable access from any public IP to the storage accounts. We recommend you to limit access to selected IPs. To limit access, enter a comma-separated list of public IP addresses, including your local machine's egress IP (to enable the completion of the Terraform run). For example: `8.8.8.8, 8.8.4.4`
10. Review the actions Terraform will perform and approve them by entering **yes**.
11. It is important to create a backup of the Terraform state file using one of the following methods:

    Back up the `terraform.tfstate` and `terraform.tfstate.backup` files or use Terraform backend to save the state.

    * Create copies of the `terraform.tfstate` and `terraform.tfstate.backup` files. These can then be moved to the working folder to allow Terraform to upgrade or destroy the created resources as necessary.

* Ensure you're using a backend block in your Terraform configuration. For more information, see the Backend block configuration overview.

The Terraform template is deployed, and your outpost is created in pending status.

To view all outposts and their details, navigate to **Settings → Data Sources & Integrations → Outposts**.

</details>

<details>

<summary>GCP</summary>

* **Prerequisites**: Before you begin, ensure you have:
  * A GCP account
  * Permission to create the required resources in Google Cloud Deployment Manager
  * Installed Terraform on your local machine. You can download Terraform from the official Terraform website and follow the installation instructions for your operating system.
  * Installed the GCP gcloud CLI tool

1. Open your local terminal (Command Prompt, PowerShell, or Terminal).
2.  Log in to your GCP account using the gcloud CLI:

    ```
    gcloud auth login
    ```
3.  Create a directory on your local machine to store and run the Terraform code. If you are creating more than one outpost, you need a separate directory for each one:

    ```
    mkdir -p ~/terraform/gcp-outpost-1
    ```
4.  Navigate to the directory you created and extract the Terraform files.

    ```
    cd ~/terraform/gcp-outpost-1
    tar -xzvf <your_template>.tar.gz
    ```
5.  Initialize Terraform in your project directory:

    ```
    terraform init
    ```
6.  Apply your Terraform configuration using the downloaded parameter file. When prompted, enter the project ID:

    ```
    terraform apply --var-file=template_params.tfvars
    ```
7. When prompted, review the actions Terraform will perform and approve them by entering **yes**.

The Terraform template is deployed, and your outpost is created in pending status.

To view all outposts and their details, navigate to **Settings → Data Sources & Integrations → Outposts**.

</details>

## Step 4. Verify the outpost

After executing the Terraform:

* **Check FICs**: In the Azure portal, go to your **App Registration → Certificates & secrets → Federated credentials**. You should see federated identity credentials created by Cortex.
* **Check Cortex XSIAM**: The outpost should appear as **Pending** in the Cortex XSIAM Outposts page at **Settings → Data Sources & Integrations → Outposts**.

The necessary permissions are granted and a notification is sent to Cortex XSIAM with the execution details.

## What's next?

Start (or continue) the CSP onboarding by running and executing the CSP onboarding wizard to generate an authentication template for the relevant CSP ([AWS](../../amazon-web-services-cloud-onboarding/onboard-amazon-web-services), [GCP](../../google-cloud-platform-cloud-onboarding/onboard-google-cloud-platform), [Azure](../../microsoft-azure-cloud-onboarding/onboard-microsoft-azure)).
