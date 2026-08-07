# Ingest network Route 53 logs from Amazon S3

You can forward network AWS Route 53 DNS logs to Cortex Cloud from Amazon Simple Storage Service (Amazon S3).

To receive network Route 53 DNS logs from Amazon S3, you must first configure data collection from Amazon S3. You can then configure the Collection Integrations settings in Cortex Cloud for Amazon S3. After you set up collection integration, Cortex Cloud begins receiving new logs and data from the source.

You can configure Amazon S3 with SQS notification using the AWS CloudFormation Script that we have created for you to make the process easier. The instructions below explain how to configure Cortex Cloud to receive network Route 53 DNS logs from Amazon S3 using SQS.

{% hint style="info" %}
**Note**

For more information on configuring data collection from Amazon S3 for Route 53 DNS logs, see the [AWS Documentation](https://aws.amazon.com/blogs/aws/log-your-vpc-dns-queries-with-route-53-resolver-query-logs/).
{% endhint %}

When Cortex Cloud begins receiving logs, the app automatically creates an Amazon Route 53 Cortex Query Language (XQL) dataset (`amazon_route53_raw`). This enables you to search the logs with XQL Search using the dataset. For example, queries refer to the in-app XQL Library. For enhanced cloud protection, you can also configure Cortex Cloud to ingest network Route 53 DNS logs as Cortex Cloud network connection stories, which you can query with XQL Search using the `xdr_data` dataset with the preset called `network_story`. Cortex Cloud can also generate Cortex Cloud issues (Analytics, Correlation Rules, IOC, and BIOC) when relevant from Amazon Route 53 DNS logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

Enhanced cloud protection provides:

* Normalization of cloud logs
* Cloud logs stitching
* Enrichment with cloud data
* Detection based on cloud analytics
* Cloud-tailored investigations

Be sure you do the following tasks before you begin configuring data collection from Amazon S3 using the AWS CloudFormation Script.

* Ensure that you have the proper permissions to run AWS CloudFormation with the script provided in Cortex Cloud. You need at a minimum the following permissions in AWS for an Amazon S3 bucket and Amazon Simple Queue Service (SQS):
  * **Amazon S3 bucket**: `GetObject`
  * **SQS**: `ChangeMessageVisibility`, `ReceiveMessage`, and `DeleteMessage`.
* Ensure that you can access your Amazon Virtual Private Cloud (VPC) and have the necessary permissions to create Route 53 Resolver Query logs.
* Determine how you want to provide access to Cortex Cloud to your logs and perform API operations. You have the following options.
  * Use Workload Federated Identity to allow Cortex Cloud's dedicated log collector service account to assume an IAM role in your AWS environment using a short-lived OIDC token, without storing any long-lived credentials. This is the Workload Federated Identity option in the Amazon S3 collection configuration and is the recommended option when available.
  * Designate an AWS IAM user, where you will need to know the Account ID for the user and have the relevant permissions to create an access key/id for the relevant IAM user. This is the default option when you configure the Amazon S3 collection by selecting Access Key.
  * Create an assumed role in AWS to delegate permissions to a Cortex Cloud AWS service. This role grants Cortex Cloud access to your flow logs. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html). This is the Assumed Role option when you configure the Amazon S3 collection in Cortex Cloud. For more information on creating an assumed role for Cortex Cloud, see [create an assumed role](create-an-assumed-role). To collect Amazon S3 logs that use server-side encryption (SSE), the user role must have an IAM policy that states that Cortex Cloud has kms:Decrypt permissions. With this permission, Amazon S3 automatically detects if a bucket is encrypted and decrypts it. If you want to collect encrypted logs from different accounts, you must have the decrypt permissions for the user role also in the key policy for the master account Key Management Service (KMS). For more information, see [Allowing users in other accounts to use a KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).
* If using Workload Federated Identity, ensure you have permissions to create an AWS IAM Identity Provider and an IAM role with a trust policy in your AWS account. You will need the Cortex Cloud service account identifier (provided in the Cortex Cloud UI after saving the configuration) to configure the trust relationship.

Configure Cortex Cloud to receive network Route 53 DNS logs from Amazon S3 using the CloudFormation Script.

1. Download the CloudFormation Script in Cortex Cloud.
   1. Navigate to Settings → Data Sources & Integrations.
   2. On the Data Sources & Integrations page, click + Add New, search for Amazon S3, then hover over it and click Add.
   3. To provide access to Cortex Cloud to your logs and to perform API operations using a designated AWS IAM user, leave the Access Key option selected. Otherwise, select Assumed Role, and ensure that you Create an Assumed Role before continuing with these instructions.
   4. For the Log Type, select Route 53 to configure your log collection to receive network Route 53 DNS logs from Amazon S3, and the following text is displayed under the field Download CloudFormation Script. See instructions here.
   5. Click the Download CloudFormation Script link to download the script to your computer.
2.  Create a new Stack in the CloudFormation Console with the script you downloaded from Cortex Cloud.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For more information on creating a Stack, see <a href="https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html">Creating a stack on the AWS CloudFormation console</a>.</p></div>

    1. Log in to the [CloudFormation Console](https://console.aws.amazon.com/cloudformation/).
    2. From the CloudFormation → Stacks page, ensure that you have selected the correct region for your configuration.
    3. Select Create Slack → With new resources (standard).
    4. Specify the template that you want AWS CloudFormation to use to create your stack. This template is the script that you downloaded from Cortex Cloud, which will create an Amazon S3 bucket, Amazon Simple Queue Service (SQS) queue, and Queue Policy. Configure the following settings in the Specify template page.
       * Prerequisite - Prepare template → Prepare template: Select Template is ready.
       * Specify Template
         * Template source: Select Upload a template file.
         * Upload a template file: Choose file, and select the `CloudFormation-Script.json` file that you downloaded.
    5. Click Next.
    6. In the Specify stack details page, configure the following stack details.
       * Stack name: Specify a descriptive name for your stack.
       * Parameters → Cortex Cloud Flow Logs Integration
         * Bucket Name: Specify the name of the S3 bucket to create, where you can leave the default populated name as xdr-route53-logs or create a new one. The name must be unique.
         * Publisher Account ID: Specify the AWS IAM user account ID with whom you are sharing access.
         * Queue Name: Specify the name for your Amazon SQS queue to create, where you can leave the default populated name as xdr-route53 or create a new one. The name must be unique.
    7. Click Next.
    8. In the Configure stack options page, there is nothing to configure, so click Next.
    9.  In the Review page, look over the stack configuration settings that you have configured and if they are correct, click Create stack. If you need to make a change, click Edit beside the particular step that you want to update.

        The stack is created and is opened with the Events tab displayed. It can take a few minutes for the new Amazon S3 bucket, SQS queue, and Queue Policy to be created. Click Refresh to get updates. Once everything is created, leave the stack opened in the current browser as you will need to access information in the stack for other steps detailed below.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For the Amazon S3 bucket created using CloudFormation, it is the customer’s responsibility to define a retention policy by creating a Lifecycle rule in the Management tab. We recommend setting the retention policy to at least 7 days to ensure the data can be retrieved under all circumstances.</p></div>
3. Configure Route 53 Query Logging in AWS.
   1. Log in to the [AWS Management Console](https://console.aws.amazon.com/).
   2. From the menu bar, ensure that you have selected the correct region for your configuration.
   3. Search for Route 53 and select Resolver → Query Logging.
   4. Configure query logging.
   5. Set the following parameters in the different sections on the Configure query logging page.
      * Query logging configuration name
        * Name: Specify a name for your Resolver query logging configuration.
      * Query logs destination
        * Destination for query logs: Select S3 bucket as the place where you want Resolver to publish query logs.
        * Amazon S3 bucket: Browse S3 to select the Amazon S3 bucket created after running the CloudFormation script, which is by default called xdr-route53-logs or select the one that you created.
      * VPCs to log queries for
        * Add VPC: Clicking the Add VPC button opens the Add VPC page, where you can choose the VPCs that you want to log queries for. When you are done, click Add.
   6. Click Configure query logging.
4.  Configure access keys for the AWS IAM user that Cortex Cloud uses for API operations.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><ul><li>It is the responsibility of the customer’s organization to ensure that the user who performs this task of creating the access key is designated with the relevant permissions. Otherwise, this can cause the process to fail with errors.</li><li>Skip this step if you are using an Assumed Role or Workload Federated Identity for Cortex Cloud.</li></ul></div>

    1. Open the [AWS IAM Console](https://console.aws.amazon.com/iam/), and in the navigation pane, select Access management → Users.
    2. Select the username of the AWS IAM user.
    3. Select the Security credentials tab, scroll down to the Access keys section, and click Create access key.
    4.  Click the copy icon next to the Access key ID and Secret access key, where you must click Show secret access key to see the secret key and record it somewhere safe before closing the window. You will need to provide these keys when you edit the Access policy of the SQS queue and when setting the AWS Client ID and AWS Client Secret in Cortex Cloud. If you forget to record the keys and close the window, you will need to generate new keys and repeat this process.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For more information, see <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html">Managing access keys for IAM users</a>.</p></div>
5.  When you create an Assumed Role, ensure that you edit the policy that defines the permissions for the role with the S3 Bucket ARN and SQS ARN, which is taken from the stack you created.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Skip this step if you are using an Access Key to provide access to Cortex Cloud.</p></div>
6. Configure the Amazon S3 collection in Cortex Cloud.
   1. Navigate to **Settings → Data Sources & Integrations**.
   2. On the **Data Sources & Integrations** page, click **+ Add New**, search for Amazon S3, then hover over it and click **Add**.
   3. Select the authentication method you configured and enter the following values:

{% tabs %}
{% tab title="Workload Federated Identity" %}
Delegates permissions to a Cortex Cloud AWS service using an IAM assumed role. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

<table><thead><tr><th width="169.71484375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the ARN of the IAM role that Cortex Cloud's log collector will assume. This role must have a trust policy that allows Cortex Cloud's service account to assume it.</td></tr><tr><td>Audience</td><td>Specify the OIDC audience value configured in your AWS IAM identity provider trust policy. This value scopes the OIDC token to your specific AWS environment.</td></tr><tr><td>Log Type</td><td>Select <strong>Route 53</strong> to configure your log collection to receive network Route 53 DNS logs from Amazon S3.</td></tr><tr><td>Use DNS logs in analytics</td><td>If selected, Cortex Cloud ingests the network Route 53 DNS logs as XDR network connection stories, which you can query using XQL Search from the <code>xdr_data</code> dataset using the preset called <code>network_story</code>.</td></tr></tbody></table>

Click **Copy Identifier** to copy the Cortex Cloud service account identifier. Add this identifier to the trust policy of the IAM role in AWS to authorize Cortex Cloud's log collector to assume the role.
{% endtab %}

{% tab title="Access Key" %}
Uses a designated AWS IAM user's static access key and secret to authenticate.

<table><thead><tr><th width="188.20703125">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>AWS Client ID</td><td>Specify the Access key ID, which you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>AWS Client Secret</td><td>Specify the Secret access key you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Route 53</strong> to configure your log collection to receive network Route 53 DNS logs from Amazon S3.</td></tr><tr><td>Use DNS logs in analytics</td><td>If selected, Cortex Cloud ingests the network Route 53 DNS logs as XDR network connection stories, which you can query using XQL Search from the <code>xdr_data</code> dataset using the preset called <code>network_story</code>.</td></tr></tbody></table>
{% endtab %}

{% tab title="Assumed Role" %}
Delegates permissions to a Cortex Cloud AWS service using an IAM assumed role. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

<table><thead><tr><th width="168.859375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the Role ARN for the Assumed Role you created in AWS.</td></tr><tr><td>External ID</td><td>Specify the External ID for the Assumed Role you created in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Route 53</strong> to configure your log collection to receive network Route 53 DNS logs from Amazon S3.</td></tr><tr><td>Use DNS logs in analytics</td><td>If selected, Cortex Cloud ingests the network Route 53 DNS logs as XDR network connection stories, which you can query using XQL Search from the <code>xdr_data</code> dataset using the preset called <code>network_story</code>.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

d. Click Test to validate access, and then click **Enable**.

Once events start to come in, a green check mark appears underneath the Amazon S3 configuration with the number of logs received.
