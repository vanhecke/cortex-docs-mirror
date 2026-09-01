---
description: Collect network flow logs from Amazon S3 in Cortex XSIAM.
---

# Ingest network flow logs from Amazon S3

You can forward network flow logs to Cortex XSIAM from Amazon Simple Storage Service (Amazon S3).

To receive network flow logs from Amazon S3, you must first configure data collection from Amazon S3. You can then configure the Data Sources & Integrations settings in Cortex XSIAM for Amazon S3. After you set up collection integration, Cortex XSIAM begins receiving new logs and data from the source.

You can either configure Amazon S3 with SQS notification manually on your own or use the AWS CloudFormation Script that we have created for you to make the process easier. The instructions below explain how to configure Cortex XSIAM to receive network flow logs from Amazon S3 using SQS. To perform these steps manually, see Configure Data Collection from Amazon S3 Manually.

{% hint style="info" %}
**Note:** For more information on configuring data collection from Amazon S3, see the Amazon S3 Documentation.
{% endhint %}

When Cortex XSIAM begins receiving logs, the app automatically creates an Amazon S3 Cortex Query Language (XQL) dataset (`aws_s3_raw`). This enables you to search the logs with XQL Search using the dataset. For example, queries refer to the in-app XQL Library. For enhanced cloud protection, you can also configure Cortex XSIAM to ingest network flow logs as Cortex XSIAM network connection stories, which you can query with XQL Search using the `xdr_data` dataset with the preset called `network_story`. Cortex XSIAM can also generate Cortex XSIAM issues (Analytics, Correlation Rules, IOC, and BIOC) when relevant from Amazon S3 logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

Enhanced cloud protection provides the following:

* Normalization of cloud logs
* Cloud logs stitching
* Enrichment with cloud data
* Detection based on cloud analytics
* Cloud-tailored investigations

Be sure you do the following tasks before you begin configuring data collection from Amazon S3 using the AWS CloudFormation Script.

* Ensure that you have the proper permissions to run AWS CloudFormation with the script provided in Cortex XSIAM. You need at a minimum the following permissions in AWS for an Amazon S3 bucket and Amazon Simple Queue Service (SQS):
  * **Amazon S3 bucket**: `GetObject`
  * **SQS**: `ChangeMessageVisibility`, `ReceiveMessage`, `GetQueueAttributes`, and `DeleteMessage`.
* Ensure that you can access your Amazon Virtual Private Cloud (VPC) and have the necessary permissions to create flow logs.
* Determine how you want to provide access to Cortex XSIAM to your logs and perform API operations. You have the following options:
  * Use Workload Federated Identity to allow Cortex XSIAM's dedicated log collector service account to assume an IAM role in your AWS environment using a short-lived OIDC token, without storing any long-lived credentials. This is the Workload Federated Identity option in the Amazon S3 collection configuration and is the recommended option when available.
  * Designate an AWS IAM user, where you will need to know the Account ID for the user and have the relevant permissions to create an access key/id for the relevant IAM user. This is the default option as explained in Configure the Amazon S3 Collection in Cortex XSIAM by selecting Access Key.
  * Create an assumed role in AWS to delegate permissions to a Cortex XSIAM AWS service. This role grants Cortex XSIAM access to your flow logs. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html). This is the Assumed Role option as described in Configure the Amazon S3 collection in Cortex XSIAM. For more information on creating an assumed role for Cortex XSIAM, see [create an assumed role](create-an-assumed-role). To collect Amazon S3 logs that use server-side encryption (SSE), the user role must have an IAM policy that states that Cortex XSIAM has kms:Decrypt permissions. With this permission, Amazon S3 automatically detects if a bucket is encrypted and decrypts it. If you want to collect encrypted logs from different accounts, you must have the decrypt permissions for the user role also in the key policy for the master account Key Management Service (KMS). For more information, see [Allowing users in other accounts to use a KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).
* If using Workload Federated Identity, ensure you have permissions to create an AWS IAM Identity Provider and an IAM role with a trust policy in your AWS account. You will need the Cortex XSIAM service account identifier (provided in the Cortex XSIAM UI after saving the configuration) to configure the trust relationship.

Configure Cortex XSIAM to receive network flow logs from Amazon S3 using the CloudFormation Script.

1. Download the CloudFormation Script in Cortex XSIAM.
   1. Navigate to Settings → Data Sources & Integrations.
   2. On the Data Sources & Integrations page, click + Add New, search for Amazon S3, then hover over it and click Add.
   3. Select the authentication method to use for Cortex XSIAM to access your logs and peform API operations:
      * To use Workload Federated Identity, select **Workload Federated Identity**. Cortex XSIAM's dedicated log collector assumes an IAM role in your AWS environment using a short-lived OIDC token, without storing any long-lived credentials. Ensure that you have created an IAM role with a trust policy before continuing.
      * To use a designated AWS IAM user with static credentials, select **Access Key**.
      * To use an IAM assumed role, select **Assumed Role**, and ensure that you [create an assumed role](create-an-assumed-role) for Cortex XSIAM before continuing with these instructions.
   4. For the Log Type, select Flow Logs to configure your log collection to receive network flow logs from Amazon S3, and the following text is displayed under the field Download CloudFormation Script. See instructions here.
   5. Click the Download CloudFormation Script link to download the script to your computer.
2.  Create a new Stack in the CloudFormation Console with the script you downloaded from Cortex XSIAM.

    For more information on creating a Stack, see [Creating a stack on the AWS CloudFormation console](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html).

    1. Log in to the [CloudFormation Console](https://console.aws.amazon.com/cloudformation/).
    2. From the CloudFormation → Stacks page, ensure that you have selected the correct region for your configuration.
    3. Select Create Stack → With new resources (standard).
    4. Specify the template that you want AWS CloudFormation to use to create your stack. This template is the script that you downloaded from Cortex XSIAM, which will create an Amazon S3 bucket, Amazon Simple Queue Service (SQS) queue, and Queue Policy. Configure the following settings in the Specify template page.
       * Prerequisite - Prepare template → Prepare template: Select Template is ready.
       * Specify Template
         * Template source: Select Upload a template file.
         *   Upload a template file: Choose file, and select the `cortex-xdr-create-s3-with-sqs-flow-logs.json` file that you downloaded from Cortex XSIAM.

             <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fu8N4bMGKrHsIn3WaUY9j%2Fcreate_stack.png?alt=media&#x26;token=0f49722a-316f-4d45-a5ad-199bd520b92f" alt=""><figcaption></figcaption></figure>
    5. Click Next.
    6. In the Specify stack details page, configure the following stack details.
       * Stack name: Specify a descriptive name for your stack.
       * Parameters → Cortex XDR Flow Logs Integration
         * Bucket Name: Specify the name of the S3 bucket to create, where you can leave the default populated name as xdr-flow-logs or create a new one. The name must be unique.
         * Publisher Account ID: Specify the AWS IAM user account ID with whom you are sharing access.
         *   Queue Name: Specify the name for your Amazon SQS queue to create, where you can leave the default populated name as xdr-flow or create a new one. The name must be unique.

             <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fl9Dd8yYtFNisFHnMtnxq%2Fspecify_stack_details.png?alt=media&#x26;token=1e8cbfa9-d692-44c2-8087-479becbc8def" alt=""><figcaption></figcaption></figure>
    7. Click Next.
    8. In the Configure stack options page, there is nothing to configure, so click Next.
    9.  In the Review page, look over the stack configurations settings that you have configured and if they are correct, click Create stack. If you need to make a change, click Edit beside the particular step that you want to update.

        The stack is created and is opened with the Events tab displayed. It can take a few minutes for the new Amazon S3 bucket, SQS queue, and Queue Policy to be created. Click Refresh to get updates. Once everything is created, leave the stack opened in the current browser, because you will need to access information in the stack for other steps detailed below.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> For the Amazon S3 bucket created using CloudFormation, it is the customer’s responsibility to define a retention policy by creating a Lifecycle rule in the Management tab. We recommend setting the retention policy to at least 7 days to ensure that the data is retrieved under all circumstances.</p></div>
3. Configure your Amazon Virtual Private Cloud (VPC) with flow logs:
   1.  Open the [Amazon VPC Console](https://console.aws.amazon.com/vpc/), and in the Resources by Region listed, select VPCs to view the VPCs configured for the current region selected. To select another VPC from another region, select See all regions, and select one of them.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> To create a new VPC, click Launch VPC Wizard. For more information, see <a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html">AWS VPC Flow Logs</a>.</p></div>
   2.  From the list of Your VPCs, select the checkbox beside the VPC that you want to configure to create flow logs, and then select Actions → Create flow log.

       <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Ffbn3IeZabZlFfT9VvhTs%2Fcreate_flow_log.png?alt=media&#x26;token=5e3a99d5-a73c-445d-9643-9ed51546829b" alt=""><figcaption></figcaption></figure>
   3. Configure the following Flow log settings:
      * Name - optional: (Optional) Specify a descriptive name for your VPC flow log.
      * Filter: Select All types of traffic to capture.
      * Maximum aggregation interval: If you anticipate a heavy flow of traffic, select 1 minute. Otherwise, leave the default setting as 10 minutes.
      * Destination: Select Send to an Amazon S3 bucket as the destination to publish the flow log data.
      *   S3 bucket ARN:Specify the Amazon Resource Name (ARN) for your Amazon S3 bucket.

          You can retrieve your bucket’s ARN by opening another instance of the AWS Management Console in a browser window and opening the [Amazon S3 console](https://console.aws.amazon.com/s3/). In the Buckets section, select the bucket that you created for collecting the Amazon S3 flow logs when you created your stack, click Copy ARN, and paste the ARN in this field.

          <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FQ0HKKosAuodsupQR3Aqk%2Fbuckets.png?alt=media&#x26;token=d682e8c4-daf9-4bc3-b94d-c4e1d8c91934" alt=""><figcaption></figcaption></figure>
      * Log record format: Select Custom Format, and in the Log Format field, specify the following fields to include in the flow log record, which you can select from the list displayed:
        * account-id
        * action
        * az-id
        * bytes
        * dstaddr
        * dstport
        * end
        * flow-direction
        * instance-id
        * interface-id
        * packets
        * log-status
        * pkt-srcaddr
        * pkt-dstaddr
        * protocol
        * region
        * srcaddr
        * srcport
        * start
        * sublocation-id
        * sublocation-type
        * subnet-id
        * tcp-flags
        * type
        * vpc-id
        * version
   4.  Click Create flow log.

       Once the flow log is created, a message indicating that the flow log was successfully created is displayed at the top of the Your VPCs page.

       In addition, if you open your Amazon S3 bucket configurations, by selecting the bucket from the [Amazon S3 console](https://console.aws.amazon.com/s3/), the Objects tab contains a folder called `AWSLogs/` to collect the flow logs.
4.  Configure access keys for the AWS IAM user that Cortex XSIAM uses for API operations.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong></p><ul><li>It is the responsibility of the customer’s organization to ensure that the user who performs this task of creating the access key is designated with the relevant permissions. Otherwise, this can cause the process to fail with errors.</li><li>Skip this step if you are using an Assumed Role or Workload Federated Identity for Cortex XSIAM.</li></ul></div>

    1. Open the [AWS IAM Console](https://console.aws.amazon.com/iam/), and in the navigation pane, select Access management → Users.
    2. Select the User name of the AWS IAM user.
    3. Select the Security credentials tab, scroll down to the Access keys section, and click Create access key.
    4. Click the copy icon next to the Access key ID and Secret access key keys, where you must click Show secret access key to see the secret key and record them somewhere safe before closing the window. You will need to provide these keys when you edit the Access policy of the SQS queue and when setting the AWS Client ID and AWS Client Secret in Cortex XSIAM. If you forget to record the keys and close the window, you will need to generate new keys and repeat this process.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> For more information, see <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html">Managing access keys for IAM users</a>.</p></div>
5.  When you create an Assumed Role in Cortex XSIAM, ensure that you edit the policy that defines the permissions for the role with the S3 Bucket ARN and SQS ARN, which is taken from the Stack you created.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Skip this step if you are using an Access Key to provide access to Cortex XSIAM.</p></div>
6. Configure the Amazon S3 collection in Cortex XSIAM.
   1. Navigate to Settings → Data Sources & Integrations.
   2. Select the Amazon S3 integration and click Add Instance.
   3. Set these parameters, where the parameters change depending on whether you configured an Access Key or Assumed Role.
      * SQS URL: Specify the SQS URL, which is taken from the stack you created. In the browser you left open after creating the stack, open the Outputs tab, copy the Value of the QueueURL and paste it in this field.
      * Name: Specify a descriptive name for your log collection configuration.
      * When setting an Access Key, set these parameters.
        * AWS Client ID: Specify the Access key ID, which you received when you created access keys for the AWS IAM user in AWS.
        * AWS Client Secret: Specify the Secret access key you received when you created access keys for the AWS IAM user in AWS.
      * When setting an Assumed Role, set these parameters.
        * Role ARN: Specify the Role ARN for the Assumed Role you created for in AWS.
        * External Id:Specify the External Id for the Assumed Role you created for in AWS.
      *   Log Type: Select Flow Logs to configure your log collection to receive network flow logs from Amazon S3. When configuring network flow log collection, the following additional field is displayed for Enhanced Cloud Protection.

          You can Normalize and enrich flow logs by selecting the checkbox. If selected, Cortex XSIAM ingests the network flow logs as network connection stories, which you can query using XQL Search from the `xdr_data` dataset using the preset called `network_story`.
   4.  Click Test to validate access, and then click Enable.

       When events start to come in, a green check mark appears underneath the Amazon S3 configuration with the number of logs received.
