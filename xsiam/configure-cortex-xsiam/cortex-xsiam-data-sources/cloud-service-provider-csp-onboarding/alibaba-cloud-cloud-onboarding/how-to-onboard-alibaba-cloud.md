# How to onboard Alibaba Cloud

{% hint style="info" %}
#### License type

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Runtime Security or Cloud Posture Security add-ons.
{% endhint %}

After completing the prerequisites, follow these instructions to onboard your Alibaba Cloud environment to Cortex XSIAM.

### Access the Alibaba Cloud onboarding wizard in Cortex XSIAM:

1. In Cortex XSIAM, select **Settings → Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click **+ Add New**.
3. On the **Add Data Sources or Integrations** page, search for **Alibaba Cloud**, then hover over it and click **Add**.

### Enter an instance name

* Enter a unique instance name or leave it empty to be automatically populated. The automatic naming convention is `ALIBABA-`\`\`. Cortex XSIAM does not prevent you from reusing instance names, but it is best practice to use a unique name for every cloud instance.

### Configure advanced settings (optional)

* Click **Show advanced settings** to define the following advanced settings:
  * **Scope Modifications:** Use these settings to fine-tune your Alibaba Cloud scope, you can modify the scope by including or excluding specific regions.
  * **Cloud Tags:** Define tags and tag values to be added to any new resource created by Cortex XSIAM in Alibaba Cloud. Note: The `managed_by = paloaltonetworks` tag is automatically added to all resources. This tag is mandatory. You cannot edit or remove this tag.

### Save the configuration

1. Click **Save**. Cortex XSIAM generates a Terraform authentication template based on the settings you configured in the Alibaba Cloud onboarding wizard.

{% hint style="info" %}
Note: If the following error appears, contact support: "Validation failed: No valid managed outpost found for cloud provider ALIBABA\_CLOUD".
{% endhint %}

2. Click **Download Terraform** to download the Terraform authentication template.

The Terraform authentication template is downloaded. To complete the process, deploy the Terraform authentication template in Alibaba Cloud.

### Deploy the authentication template

{% hint style="info" %}
#### Prerequisites

Before you begin, ensure you have:

* Installed Terraform on your local machine. You can download Terraform from the official [Terraform website](https://www.terraform.io/downloads.html) and follow the installation instructions for your operating system.
* Installed the [Alibaba Cloud CLI](https://www.alibabacloud.com/help/en/cli/installation-guide/) tool.
{% endhint %}

1. Log in to your Alibaba Cloud console and open [Cloud Shell](https://www.alibabacloud.com/products/cloud-shell).
2.  Create a directory on your local machine to store and run the Terraform code. If you have more than one Alibaba Cloud cloud instance, you need a separate directory for each one:

    ```
    mkdir -p ~/terraform/alibaba-cloud-connector-1
    ```
3.  Navigate to the directory you created and extract the Terraform files from the compressed archive you downloaded previously. Ensure all necessary Terraform files are present (main.tf, template\_params.tfvars, and so on).

    #### Important

    Do not delete or move the Terraform files from this folder. It will prevent you from being able to [edit your cloud instance](../edit-your-onboarded-csp-configuration) in the future.

    ```
    cd ~/terraform/alibaba-cloud-connector-1
    tar -xzvf <your_template>.tar.gz.
    ```
4.  Initialize Terraform in your project directory:

    ```
    terraform init
    ```
5.  Apply your Terraform configuration using the downloaded parameter file:

    ```
    terraform apply --var-file=template_params.tfvars
    ```
6. When prompted, review the actions the Terraform will perform and approve them by entering yes.

The Terraform template is deployed. To complete the onboarding of your Alibaba Cloud environment, proceed to [manually connect the pending cloud instance](../manually-connect-a-cloud-instance).
