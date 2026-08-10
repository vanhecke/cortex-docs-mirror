---
description: >-
  Learn how to deploy the Terraform or CloudFormation authentication template in
  Amazon Web Services.
---

# Deploy the authentication template in AWS

To connect your AWS account to Cortex XSIAM, you must deploy an authentication template. The deployment method you use depends on the template type you downloaded from the AWS onboarding wizard.

{% tabs %}
{% tab title="CloudFormation" %}
When you select to manually deploy the authentication template, you must connect to AWS Management Console to create a stack using the template file.

1. In AWS Management Console, navigate to [CloudFormation](https://console.aws.amazon.com/cloudformation/).
2. On the **Stacks** page, click **Create stack**, and then select **With new resources (standard)**.
3. On the **Create stack** page, in **Prerequisite - Prepare template**, select **Choose an existing template**.
4. In **Specify template**, select **Upload a template file**, then click **Choose file** and upload the template downloaded from Cortex XSIAM. Click **Next**.
5. In the **Specify stack details** page, enter a **Stack name**.
6. In **Parameters**, review the values pre-populated by Cortex XSIAM: **ExternalID**, **OutpostRoleArn**, and **CortexPlatformRoleName**. If you have enabled custom Control Tower audit log collection, the following pre-populated values are also displayed: **SqsQueueName** and **CloudTrailReadRoleName**. Do not change these values. The **ExternalID** is unique to your Cortex XSIAM tenant and acts as a shared secret in the role's trust policy. Replacing it will prevent Cortex XSIAM from assuming the role.
7. In **Parameters**, if you have enabled custom log collection, enter the following details:
   * `CloudTrailKmsArn`**:** (Optional) The ARN of the AWS KMS key used to encrypt the CloudTrail log files, if using.
   * `CloudTrailLogBucket`**:** The name of the Amazon S3 bucket where CloudTrail stores the log files.
   * `CloudTrailSnsArn`**:** The ARN of the Amazon SNS topic that CloudTrail uses to send notifications when new log files are delivered.
   * `LoggingAccountId`: (Only for custom Control Tower BYOB) The AWS Account ID of the dedicated AWS Control Tower logging account where the centralized S3 bucket resides.
   * `SnsTopicOuId`: (Only for custom Control Tower BYOB) OU containing the SNS topic account.
   * `LoggingAccountOuId`: (Only for custom Control Tower BYOB) OU containing the Log Archive account.
   * `OrganizationalUnitId`: (Only for organization or organizational unit scope) Organizational root ID.
8. Click **Next** and **Next** again.
9. In **Review**, in the **Capabilities** section, acknowledge that CloudFormation might create IAM resources with custom names and click Submit. (This is required because the template creates the IAM roles Cortex XSIAM uses to access your account.) The stack is complete when it appears in the Stacks list with status of **CREATE\_COMPLETE**.

When the template is successfully uploaded to AWS and the stack creation is complete, a Lambda function notifies Cortex XSIAM and the cloud instance will appear as **Connected**. The initial discovery scan is then started. When the scan is complete, you can view the discovered assets in **Asset Inventory**.
{% endtab %}

{% tab title="Terraform" %}
Downloading a Terraform template is only available for AWS account scope.

{% hint style="info" %}
#### Prerequisites

Before you begin, ensure you have:

* Write permissions to your target AWS account.
* Installed Terraform on your local machine. You can download Terraform from the official [Terraform website](https://www.terraform.io/downloads.html) and follow the installation instructions for your operating system.
* Installed and configured the [AWS CLI](#cloudformation) on your local machine with active credentials for your target AWS account.
* Reviewed the [introduction to Terraform for Cloud service provider (CSP) onboarding](../introduction-to-terraform-for-cloud-service-provider-csp-onboarding) to understand the underlying logic of how Terraform interacts with your cloud environment.
{% endhint %}

1. Open your local terminal (Command prompt, PowerShell, or Terminal).
2.  Log in to your AWS account using the AWS CLI:

    ```
    aws login
    ```
3. Create a directory on your local machine to store and run the Terraform code. If you have more than one AWS connector, you need a separate directory for each one:

```
mkdir -p ~/terraform/aws-connector-1

```

4. Navigate to the directory you created and extract the Terraform files. Ensure all necessary Terraform files are present (`main.tf`, `template_params.tfvars`, etc).

{% hint style="warning" %}
You must not delete or move the Terraform files from this folder. It will prevent you from being able to [edit your cloud instance](../edit-your-onboarded-csp-configuration) in the future.
{% endhint %}

```
cd ~/terraform/aws-connector-1
tar -xzvf <your_template>.tar.gz
```

5. Initialize Terraform in your project directory:

```
terraform init
```

6. Apply your Terraform configuration using the downloaded parameter file. :

```
terraform apply --var-file=template_params.tfvars
```

7. If you selected custom audit log collection, Terraform prompts for:
   * `cloud_trail_logs_bucket`: The name of the Amazon S3 bucket where CloudTrail stores the log files.
   * `cloud_trail_sns_arn`: The ARN of the Amazon SNS topic that CloudTrail uses to send notifications when new log files are delivered.
   * `cloud_trail_kms_arn`: (Optional) The ARN of the AWS KMS key used to encrypt the CloudTrail log files, if using.

When the template is successfully deployed, a Lambda function notifies Cortex XSIAM and the cloud instance will appear as **Connected**. The initial discovery scan is then started. When the scan is complete, you can view the discovered assets in **Asset Inventory**.
{% endtab %}
{% endtabs %}
