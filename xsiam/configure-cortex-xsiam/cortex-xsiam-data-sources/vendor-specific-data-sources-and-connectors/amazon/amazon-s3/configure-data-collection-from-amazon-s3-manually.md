# Configure data collection from Amazon S3 manually

There are various reasons why you may need to configure data collection from Amazon S3 manually, as opposed to using the CloudFormation Script provided in Cortex XSIAM. For example, if your organization does not use CloudFormation scripts, you will need to follow the instructions below, which explain at a high-level how to perform these steps manually with a link to the relevant topic in the Amazon S3 documentation with the detailed steps to follow.

As soon as Cortex XSIAM begins receiving logs, the app automatically creates an Amazon S3 Cortex Query Language (XQL) dataset (`aws_s3_raw`). This enables you to search the logs with XQL Search using the dataset. For example queries, refer to the in-app XQL Library. For enhanced cloud protection, you can also configure Cortex XSIAM to ingest network flow logs as Cortex XSIAM network connection stories, which you can query with XQL Search using the `xdr_dataset` dataset with the preset called `network_story`. Cortex XSIAM can also generate Cortex XSIAM issues (Analytics, Correlations, IOC, and BIOC) when relevant from Amazon S3 logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

Enhanced cloud protection provides:

* Normalization of cloud logs
* Cloud logs stitching
* Enrichment with cloud data
* Detection based on cloud analytics
* Cloud-tailored investigations

Be sure you do the following tasks before you begin configuring data collection manually from Amazon CloudWatch to Amazon S3.

{% hint style="info" %}
**Note:** If you already have an Amazon S3 bucket configured with VPC flow logs that you want to use for this configuration, you do not need to perform the prerequisite steps detailed in the first two bullets.
{% endhint %}

* Ensure that you have at a minimum the following permissions in AWS for an Amazon S3 bucket and Amazon Simple Queue Service (SQS).
  * **Amazon S3 bucket**: `GetObject`
  * **SQS**: `ChangeMessageVisibility`, `ReceiveMessage`, and `DeleteMessage`.
*   Create a dedicated Amazon S3 bucket for collecting network flow logs with the default settings. For more information, see [Creating a bucket using the Amazon S3 Console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>It is your responsibility to define a retention policy for your Amazon S3 bucket by creating a Lifecycle rule in the Management tab. We recommend setting the retention policy to at least 7 days to ensure that the data can be retrieved under all circumstances.</p></div>
* Ensure that you can access your Amazon Virtual Private Cloud (VPC) and have the necessary permissions to create flow logs.
* Determine how you want to provide access to Cortex XSIAM to your logs and perform API operations. You have the following options.
  * Use Workload Federated Identity to allow Cortex XSIAM's dedicated log collector service account to assume an IAM role in your AWS environment using a short-lived OIDC token, without storing any long-lived credentials. This is the Workload Federated Identity option in the Amazon S3 collection configuration and is the recommended option when available.
  * Designate an AWS IAM user, where you will need to know the Account ID for the user and have the relevant permissions to create an access key/id for the relevant IAM user. This is the default option as explained in Configure the Amazon S3 collection by selecting Access Key.
  * Create an assumed role in AWS to delegate permissions to a Cortex XSIAM AWS service. This role grants Cortex XSIAM access to your flow logs. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html). This is the Assumed Role option as described in the Configure the Amazon S3 collection. For more information on creating an assumed role for Cortex XSIAM, see [Create an assumed role](create-an-assumed-role). To collect Amazon S3 logs that use server-side encryption (SSE), the user role must have an IAM policy that states that Cortex XSIAM has kms:Decrypt permissions. With this permission, Amazon S3 automatically detects if a bucket is encrypted and decrypts it. If you want to collect encrypted logs from different accounts, you must have the decrypt permissions for the user role also in the key policy for the master account Key Management Service (KMS). For more information, see [Allowing users in other accounts to use a KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).
* If using Workload Federated Identity, ensure you have permissions to create an AWS IAM Identity Provider and an IAM role with a trust policy in your AWS account. You will need the Cortex XSIAM service account identifier (provided in the Cortex XSIAM UI after saving the configuration) to configure the trust relationship.

{% hint style="info" %}
**Note:** For resources such as Amazon S3, SQS, VPC flow logs, and event notifications, you may use the default configurations; yet, these settings remain fully customizable to meet your specific environment requirements.
{% endhint %}

Configure Cortex XSIAM to receive network flow logs from Amazon S3 manually.

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/).
2. From the menu bar, ensure that you have selected the correct region for your configuration.
3.  Configure your Amazon Virtual Private Cloud (VPC) with flow logs. For more information, see [AWS VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html).

    If you already have an Amazon S3 bucket configured with VPC flow logs, skip this step and go to Configure an Amazon Simple Queue Service (SQS).
4.  Configure an Amazon Simple Queue Service (SQS). For more information, see [Configuring Amazon SQS queues (console)](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-configuring.html).

    Ensure that you create your Amazon S3 bucket and Amazon SQS queue in the same region.
5. Configure an event notification to your Amazon SQS whenever a file is written to your Amazon S3 bucket. For more information, see [Amazon S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html).
6. Configure access keys for the AWS IAM user that Cortex XSIAM uses for API operations. For more information, see [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
   * It is the responsibility of the customer’s organization to ensure that the user who performs this task of creating the access key is designated with the relevant permissions. Otherwise, this can cause the process to fail with errors.
   * Skip this step if you are using an Assumed Role or Workload Federated Identity for Cortex XSIAM.
7.  Update the Access Policy of your SQS queue and grant the required permissions mentioned above to the relevant IAM user. For more information, see [Granting permissions to publish event notification messages to a destination](https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html).

    Skip this step if you are using an Assumed Role or Workload Federated Identity for Cortex XSIAM.
8. Configure the Amazon S3 collection in Cortex XSIAM.
   1. Navigate to **Settings → Data Sources & Integrations**.
   2. On the **Data Sources & Integrations** page, click **+ Add New**, search for Amazon S3, then hover over it and click **Add**.
   3. Select the authentication method you configured and enter the following values:

{% tabs %}
{% tab title="Workload Federated Identity" %}
Delegates permissions to a Cortex XSIAM AWS service using an IAM assumed role. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

<table><thead><tr><th width="169.71484375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the ARN of the IAM role that Cortex Cloud's log collector will assume. This role must have a trust policy that allows Cortex Cloud's service account to assume it.</td></tr><tr><td>Audience</td><td>Specify the OIDC audience value configured in your AWS IAM identity provider trust policy. This value scopes the OIDC token to your specific AWS environment.</td></tr><tr><td>Log Type</td><td>Select <strong>Flow Logs</strong> to configure your log collection to receive network flow logs from Amazon S3.</td></tr></tbody></table>

Click **Copy Identifier** to copy the Cortex XSIAM service account identifier. Add this identifier to the trust policy of the IAM role in AWS to authorize Cortex XSIAM's log collector to assume the role.
{% endtab %}

{% tab title="Access Key" %}
Uses a designated AWS IAM user's static access key and secret to authenticate.

<table><thead><tr><th width="188.20703125">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>AWS Client ID</td><td>Specify the Access key ID, which you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>AWS Client Secret</td><td>Specify the Secret access key you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Flow Logs</strong> to configure your log collection to receive network flow logs from Amazon S3.</td></tr></tbody></table>
{% endtab %}

{% tab title="Assumed Role" %}
Delegates permissions to a Cortex XSIAM AWS service using an IAM assumed role. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

<table><thead><tr><th width="168.859375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the Role ARN for the Assumed Role you created in AWS.</td></tr><tr><td>External ID</td><td>Specify the External ID for the Assumed Role you created in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Flow Logs</strong> to configure your log collection to receive network flow logs from Amazon S3.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

4. Click Test to validate access, and then click Enable.

Once events start to come in, a green check mark appears underneath the Amazon S3 configuration with the number of logs received.
