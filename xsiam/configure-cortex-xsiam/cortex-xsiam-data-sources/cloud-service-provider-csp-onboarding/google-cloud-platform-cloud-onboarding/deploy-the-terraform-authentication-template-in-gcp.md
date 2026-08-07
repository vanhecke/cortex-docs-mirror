---
description: >-
  Learn how to deploy the Terraform authentication template in Google Cloud
  Console.
---

# Deploy the Terraform authentication template in GCP

When you have downloaded the Terraform template file in the onboarding wizard, you must connect to Google Cloud Console to create a stack using the template file.

{% hint style="info" %}
Prerequisites

Before you begin, ensure you have:

* A GCP account.
* Permission to create the required resources in Google Cloud Deployment Manager.
* Installed Terraform on your local machine. You can download Terraform from the official [Terraform website](https://www.terraform.io/downloads.html) and follow the installation instructions for your operating system.
* Installed the [GCP gcloud CLI tool](https://cloud.google.com/sdk/docs/install#linux).
* Reviewed the [introduction to Terraform for Cloud service provider (CSP) onboarding](../introduction-to-terraform-for-cloud-service-provider-csp-onboarding) to understand the underlying logic of how Terraform interacts with your cloud environment.
{% endhint %}

1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your GCP account using the gcloud CLI:

    ```
    gcloud auth login
    ```
3. Create a directory on your local machine to store and run the Terraform code. If you have more than one GCP connector, you need a separate directory for each one:

```
mkdir -p ~/terraform/gcp-connector-1
```

4. Navigate to the directory you created and extract the Terraform files. Ensure all necessary Terraform files are present (`main.tf`, `template_params.tfvars`, etc).

{% hint style="warning" %}
You must not delete or move the Terraform files from this folder. It will prevent you from being able to [edit your cloud instance](../edit-your-onboarded-csp-configuration) in the future.
{% endhint %}

```
cd ~/terraform/gcp-connector-1
tar -xzvf <your_template>.tar.gz
```

5. Initialize Terraform in your project directory:

```
terraform init
```

6. Apply your Terraform configuration using the downloaded parameter file. When prompted, enter the project ID if you configured one in the onboarding wizard:

```
terraform apply --var-file=template_params.tfvars
```

The Terraform template is deployed.

When the template is successfully uploaded to GCP, the initial discovery scan is started. When the scan is complete, you can view your cloud assets in **Asset Inventory**.
