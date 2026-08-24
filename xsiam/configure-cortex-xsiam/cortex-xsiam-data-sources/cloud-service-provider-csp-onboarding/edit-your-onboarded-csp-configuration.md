---
description: Update onboarded cloud configurations in Cortex XSIAM.
---

# Edit your onboarded CSP configuration

In order to make changes to your onboarded CSP configuration, you first modify the cloud instance settings in Cortex Cloud and download an updated authentication template. After uploading the updated template to the CSP environment, you execute the template and then the changes take affect.

1. Navigate to **Settings → Data Sources & Integrations**.
2. Identify the Cloud Service Provider you want to update and click **View Details**.
3. In the **Cloud Instances** page, identify the cloud instance you want to edit and click the **Configuration** pencil icon to edit the instance.
4.  Make changes to the configuration settings. Click **Save**.

    If the changes you made require re-deploying the authentication template, you will be prompted to to download the file. Click **Download CloudFormation** or **Download Terraform** as relevant to your CSP type.

{% hint style="warning" %}
#### Important

When using Terraform authentication templates, you must execute the updated Terraform template from the same folder where the original Terraform template was executed.
{% endhint %}

5. On the **Cloud Instances** page, a notification appears stating that there are pending changes for the cloud instance you updated. These changes are not applied until you execute the updated template in the CSP environment.\
   While a cloud instance has pending changes, you can manage those changes using the following options:
   * **Revoke pending changes:** Discard the pending changes and return the cloud instance to the last successfully executed state. After you revoke pending changes, the cloud instance exits the _Pending Changes_ state and no template reexecution is required.
   * **Edit pending changes:** The configuration wizard opens and displays the current pending changes. Use this option to continue editing from the pending state rather than starting from the last executed configuration. For example, if you added a capability, saved the updated template, and did not yet execute the template in the CSP, selecting **Edit pending changes** opens the wizard with that capability already selected.
6. Execute the updated authentication template in your CSP environment by selecting the appropriate procedure below.

{% tabs %}
{% tab title="AWS CloudFormation" %}
After you have downloaded the updated CloudFormation authentication template, connect to AWS Management Console to perform a direct update to the stack using the updated template file. With a direct update, you submit a template or input parameters that specify updates to the resources in the stack, and CloudFormation immediately deploys them.

1. Log in to the AWS Management Console and open the [CloudFormation console](https://console.aws.amazon.com/cloudformation/).
2. On the **Stacks** page, select the existing stack that you want to update.
3. In the stack details pane, select **Update stack → Make a direct update.**
4. On the **Update stack** page, select **Replace existing template**.
5. Under **Specify template**, select **Upload a template file**. Select the updated authentication template you downloaded from Cortex Cloud.
6. Click **Next** and **Next** again.
7. Select to acknowledge that AWS CloudFormation might create IAM resources with custom names. Click **Next**.
8. Click **Submit**. The stack update is complete when it appears in the Stacks list with status of **UPDATE\_COMPLETE**.
{% endtab %}

{% tab title="AWS Terraform" %}
Using a Terraform template is only available for AWS account scope. After you have downloaded the updated Terraform template file, log in to your AWS account using the AWS CLI:

1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your AWS account using the AWS CLI:

    ```
    aws login
    ```
3.  Navigate to the directory you originally used for the Terraform template when onboarding your CSP and extract the Terraform files.

    ```
    cd ~/terraform/aws-connector-1
    tar -xzvf <your_template>.tar.gz
    ```
4.  Initialize the upgrade of the Terraform in your project directory:

    ```
    terraform init -upgrade
    ```
5.  Apply your Terraform configuration using the downloaded parameter file:

    ```
    terraform apply --var-file=template_params.tfvars
    ```

The updated Terraform template is deployed.
{% endtab %}

{% tab title="GCP" %}
After you have downloaded the updated Terraform template file, connect to Google Cloud Console to update the stack using the updated template file.

1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your GCP account using the gcloud CLI:

    ```
    gcloud auth login
    ```
3.  Navigate to the directory you originally used for the Terraform template when onboarding your CSP and extract the Terraform files.

    ```
    cd ~/terraform/gcp-connector-1
    tar -xzvf <your_template>.tar.gz
    ```
4.  Initialize the upgrade of the Terraform in your project directory:

    ```
    terraform init -upgrade
    ```
5.  Apply your Terraform configuration using the downloaded parameter file. When prompted, enter the project ID if you configured one in the onboarding wizard:

    ```
    terraform apply --var-file=template_params.tfvars
    ```

    The updated Terraform template is deployed.
{% endtab %}

{% tab title="Azure ARM using CLI" %}
After you have downloaded the updated authentication template file, lot in to Azure portal to update the stack using the updated template file.

1. Log in to the Azure portal. Select Cloud Shell from the top navigation and then select Bash.
2.  Navigate to the directory you originally used for the authentication template when onboarding your CSP and extract the files.

    ```
    cd ~/azure-connector-1
    tar -xzvf <your_template>.tar.gz.
    ```
3.  In Cloud Shell, run the onboard.sh file:

    ```
    bash onboard.sh
    ```

    The updated authentication template is deployed.
{% endtab %}

{% tab title="Azure subscriptions" %}
After you have downloaded the updated authentication template file, use the same method you used initially to execute the template in Microsoft Azure:

#### Execute the Terraform authentication template

1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your Azure account using the Azure CLI:

    ```
    az login
    ```
3.  Navigate to the directory you originally used for the Terraform template when onboarding your CSP and extract the Terraform files.

    ```
    cd ~/terraform/azure-connector-1
    tar -xzvf <your_template>.tar.gz.
    ```
4.  Initialize the upgrade of the Terraform in your project directory:

    ```
    terraform init -upgrade
    ```
5.  Apply your Terraform configuration using the downloaded parameter file. :

    ```
    terraform apply --var-file=template_params.tfvars
    ```

    The updated Terraform template is deployed.

#### Deploy the authentication template in Azure Resource Manager

1. Open your local terminal.
2.  Log in to your Azure account using the Azure CLI:

    ```
    az login
    ```
3.  Deploy the updated template file:

    ```
    az deployment sub create  --location <LOCATION>  --subscription <SUBSCRIPTION_ID> --template-file <JSON_TEMPLATE> 
    ```

    where:

    * `<LOCATION>` is the location of the resource group. (For example, eastus or westus.)
    * `<SUBSCRIPTION_ID>` is the ID of the subscription you want to onboard.
    * `<JSON_TEMPLATE>` is the JSON template file that you downloaded at the end of the onboarding wizard.

    The updated template is deployed.

<br>
{% endtab %}
{% endtabs %}
