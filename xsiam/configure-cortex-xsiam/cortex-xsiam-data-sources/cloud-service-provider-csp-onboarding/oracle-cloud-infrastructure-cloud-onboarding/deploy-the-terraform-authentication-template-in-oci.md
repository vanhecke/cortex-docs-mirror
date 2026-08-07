---
description: >-
  Learn how to deploy the Terraform authentication template in Oracle Cloud
  Infrastructure.
---

# Deploy the Terraform authentication template in OCI

When you have downloaded the Terraform template file in the onboarding wizard, you must connect to Oracle Cloud Infrastructure (OCI) CLI tool to deploy the template file. For more information about the OCI CLI tool, refer [Oracle documentation](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/cliconcepts.htm). to create a stack using the template file.

#### Prerequisite

{% hint style="info" %}
Prerequisites

Before you begin, ensure you have:

* An Oracle Cloud Infrastructure account and the tenancy OCID.
* Permission to deploy a custom template and create its resources in OCI.
* Installed Terraform on your local machine. You can download Terraform from the official [Terraform website](https://www.terraform.io/downloads.html) and follow the installation instructions for your operating system.
* Installed the OCI CLI tool, and authenticated with a key pair or token-based credentials.
* Reviewed the [introduction to Terraform for Cloud service provider (CSP) onboarding](../introduction-to-terraform-for-cloud-service-provider-csp-onboarding) to understand the underlying logic of how Terraform interacts with your cloud environment.
{% endhint %}

1. Log in to [OCI](https://www.oracle.com/il-en/cloud/sign-in.html) and open Cloud Shell.
2.  Create a directory on your local machine to store and run the Terraform code. If you have more than one OCI connector, you need a separate directory for each one. For example:

    ```
    mkdir -p ~/terraform/oci-connector-1
    ```
3.  Navigate to the directory you created and extract the Terraform files. Ensure all necessary Terraform files are present (`main.tf`, `template_params.tfvars`, and so on). For example:

    ```
    cd ~/terraform/oci-connector-1
    tar -xzvf <your_template>.tar.gz.
    ```
4.  Initialize Terraform in your project directory:

    ```
    terraform init
    ```

    It might take several seconds until the initialization is complete.
5.  Apply your Terraform configuration using the downloaded parameter file. When prompted to enter a value, enter the tenancy OCID.

    ```
    terraform apply --var-file=template_params.tfvars
    ```
6.  When prompted, review the actions the Terraform will perform, and approve them by entering **`yes`**.

    The Terraform template is deployed.
7.  Since non-default domains are bound to a specific home region, you must manually enable replication to interact with domain resources across different geographical regions. To enable replication:

    1. Open the Oracle Cloud Console and log in.
    2. Open the main navigation menu and select **Identity & Security → Identity → Domains**.
    3. Select the name of the **Identity Domain** created by the Terraform script you downloaded from Cortex XSIAM.
    4. On the domain details page, go to the region section and click the **Actions** menu (three dots) for the target region you need to collect resources from.
    5. Select **Enable replication** and confirm.

    Replication may take up to 60 minutes depending on the complexity of your identity setup.

Once the status changes from **Enabling** to **Enabled**, the domain is ready to handle identities in that specific region.

When the template is successfully uploaded to GCP, the initial discovery scan is started. When the scan is complete, you can view your cloud assets in **Asset Inventory**.
