---
description: Collect generic logs from Amazon S3 in Cortex XSIAM.
---

# Ingest generic logs from Amazon S3

You can forward generic logs for the relevant service to Cortex XSIAM from Amazon S3.

To receive generic data from Amazon Simple Storage Service (Amazon S3), you must first configure data collection from Amazon S3. You can then configure the Data Sources & Integrations settings in Cortex XSIAM for Amazon S3. After you set up collection integration, Cortex XSIAM begins receiving new logs and data from the source.

{% hint style="info" %}
**Note:** For more information on configuring data collection from Amazon S3, see the Amazon S3 Documentation.
{% endhint %}

When Cortex XSIAM begins receiving logs, the app automatically creates an Amazon S3 Cortex Query Language (XQL) dataset (`<Vendor>_<Product>_raw`). This enables you to search the logs using XQL Search with the dataset. For example queries, refer to the in-app XQL Library. Cortex XSIAM can also generate Cortex XSIAM issues (Correlation Rules only), when relevant, from Amazon S3 logs.

{% hint style="info" %}
**Note:** You need to set up an Amazon S3 data collector to receive generic logs when collecting logs from BeyondTrust Privilege Management Cloud. For more information, see [Ingest logs from BeyondTrust Privilege Management Cloud](../../beyondtrust/beyondtrust-privilege-management-cloud/ingest-logs-from-beyondtrust-privilege-management-cloud).
{% endhint %}

#### Prerequisites

Perform the following tasks before you begin configuring data collection from Amazon S3:

*   Create a dedicated Amazon S3 bucket, which collects the generic logs that you want to capture. For more information, see [Creating a bucket using the Amazon S3 Console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> It is the customer’s responsibility to define a retention policy for your Amazon S3 bucket by creating a Lifecycle rule in the Management tab. We recommend setting the retention policy to at least 7 days to ensure that the data is retrieved under all circumstances.</p></div>
* The logs collected by your dedicated Amazon S3 bucket must adhere to the following guidelines.
  * Each log file must use the 1 log per line format. By default, multi-line format is not supported. It can only be used for `raw` format when you specifically configure your environment for that use case.
  * The log format must be compressed as gzip or uncompressed.
  * For best performance, we recommend limiting each file size to up to 50 MB (compressed).
* Ensure that you have at a minimum the following permissions in AWS for an Amazon S3 bucket and Amazon Simple Queue Service (SQS).
  * **Amazon S3 bucket**: `GetObject`
  * **SQS**: `ChangeMessageVisibility`, `ReceiveMessage`, `GetQueueAttributes`, and `DeleteMessage`.
* Determine how you want to provide access to Cortex XSIAM to your logs and perform API operations. You have the following options:
  * Use Workload Federated Identity to allow Cortex XSIAM's dedicated log collector service account to assume an IAM role in your AWS environment using a short-lived OIDC token, without storing any long-lived credentials. This is the Workload Federated Identity option in the Amazon S3 collection configuration and is the recommended option when available.
  * Designate an AWS IAM user, where you will need to know the Account ID for the user and have the relevant permissions to create an access key/id for the relevant IAM user.
  * Create an assumed role in AWS to delegate permissions to a Cortex XSIAM AWS service. This role grants Cortex XSIAM access to your flow logs. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html). This is the Assumed Role option described in the configure the Amazon S3 collection in Cortex XSIAM. For more information on creating an assumed role for Cortex XSIAM, see [Create an assumed role](create-an-assumed-role).
* If using Workload Federated Identity, ensure you have permissions to create an AWS IAM Identity Provider and an IAM role with a trust policy in your AWS account. You will need the Cortex XSIAM service account identifier (provided in the Cortex XSIAM UI after saving the configuration) to configure the trust relationship.
* To collect Amazon S3 logs that use server-side encryption (SSE), the user role must have an IAM policy that states that Cortex XSIAM has kms:Decrypt permissions. With this permission, Amazon S3 automatically detects if a bucket is encrypted and decrypts it. If you want to collect encrypted logs from different accounts, you must have the decrypt permissions for the user role also in the key policy for the master account Key Management Service (KMS). For more information, see [Allowing users in other accounts to use a KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).

Configure Cortex XSIAM to receive generic logs from Amazon S3:

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/).
2. From the menu bar, ensure that you have selected the correct region for your configuration.
3.  Configure an Amazon Simple Queue Service (SQS).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Ensure that you create your Amazon S3 bucket and Amazon SQS queue in the same region.</p></div>

    1. In the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), click Create Queue.
    2. Configure the following settings, where the default settings should be used unless otherwise indicated.
       * Type: Select Standard queue (default).
       * Name: Specify a descriptive name for your SQS queue.
       * Configuration section: Leave the default settings for the various fields.
       *   Access policy → Choose method: Select Advanced and update the Access policy code in the editor window to enable your Amazon S3 bucket to publish event notification messages to your SQS queue. Use this sample code as a guide for defining the `“Statement”` with the following definitions.<br>

           -**`“Resource”`**: Leave the automatically generated ARN for the SQS queue that is set in the code, which uses the format `“arn:sns:Region:account-id:topic-name”`.<br>

           You can retrieve your bucket’s ARN by opening the [Amazon S3 Console](https://console.aws.amazon.com/s3/) in a browser window. In the Buckets section, select the bucket that you created for collecting the Amazon S3 flow logs, click Copy ARN, and paste the ARN in the field.

           <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FNfdJ80j5Sg9zws5TKgVz%2Fcopy_arn.png?alt=media&#x26;token=80e58b48-9710-430d-bce6-d22ef7d38195" alt=""><figcaption></figcaption></figure>

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> For more information on granting permissions to publish messages to an SQS queue, see <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html">Granting permissions to publish event notification messages to a destination</a>.</p></div>

           ```
           {
             "Version": "2012-10-17",
             "Statement": [
               {
                 "Effect": "Allow",
                 "Principal": {
                   "Service": "s3.amazonaws.com"
                 },
                 "Action": "SQS:SendMessage",
                 "Resource": "[Leave automatically generated ARN for the SQS queue defined by AWS]",
                 "Condition": {
                   "ArnLike": {
                     "aws:SourceArn": "[ARN of your Amazon S3 bucket]"
                   }
                 }
               }
             ]
           }
           ```
       * Dead-letter queue section: We recommend that you configure a queue for sending undeliverable messages by selecting Enabled, and then in the Choose queue field selecting the queue to send the messages. You may need to create a new queue for this, if you do not already have one set up. For more information, see [Amazon SQS dead-letter queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html).
    3.  Click Create queue.

        Once the SQS is created, a message indicating that the queue was successfully configured is displayed at the top of the page.
4. Configure an event notification to your Amazon SQS whenever a file is written to your Amazon S3 bucket.
   1. Open the [Amazon S3 Console](https://console.aws.amazon.com/s3/) and in the Properties tab of your Amazon S3 bucket, scroll down to the Event notifications section, and click Create event notification.
   2. Configure the following settings:
      * Event name: Specify a descriptive name for your event notification containing up to 255 characters.
      * Prefix: Do not set a prefix, as the Amazon S3 bucket is meant to be a dedicated bucket for collecting only network flow logs.
      * Event types: Select All object create events for the type of event notifications that you want to receive.
      * Destination: Select SQS queue to send notifications to an SQS queue to be read by a server.
      *   Specify SQS queue: You can either select Choose from your SQS queues and then select the SQS queue, or select Enter SQS queue ARN and specify the ARN in the SQS queue field.

          You can retrieve your SQS queue ARN by opening another instance of the AWS Management Console in a browser window, and opening the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), and selecting the Amazon SQS that you created. In the Details section, under ARN, click the copy icon (<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAATCAYAAAB2pebxAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QYcBzsjhEi12QAAAIlJREFUOI1j/P///38GCgETpQYMLkNYsAnWt3YzXLt+i6BmbU11hobqEuwuIcYABgYGhqvXb+J2CQysXjIbp1xoTCqcDTcEmxeQFcIAzAvIAO4dUr2ADDC8Q6wXsLqEEjDEDUEPG4pcoqWpxsDAQCCx4QLoMYhhCK5oxAfg3oE5jRDApo6RGiUbANIcKtiGO7bCAAAAAElFTkSuQmCC" alt="copy-icon.png" data-size="line">), and paste the ARN in the field.

          <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgn8kkkPUoaMoehPVszIe%2Fxdr-flow.png?alt=media&#x26;token=86c9e338-9f2a-4845-b83c-d02400208832" alt=""><figcaption></figcaption></figure>
   3.  Click Save changes.

       Once the event notification is created, a message indicating that the event notification was successfully created is displayed at the top of the page.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> If your receive an error when trying to save your changes, you should ensure that the permissions are set up correctly.</p></div>
5.  Configure access keys for the AWS IAM user.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong></p><ul><li>It is the responsibility of your organization to ensure that the user who performs this task of creating the access key is assigned the relevant permissions. Otherwise, this can cause the process to fail with errors.</li><li>Skip this step if you are using an Assumed Role or Workload Federated Identity for Cortex XSIAM.</li></ul></div>

    1. Open the [AWS IAM Console](https://console.aws.amazon.com/iam/), and in the navigation pane, select Access management → Users.
    2. Select the username of the AWS IAM user.
    3. Select the Security credentials tab, scroll down to the Access keys section, and click Create access key.
    4.  Click the copy icon () next to the Access key ID and Secret access key. You must click Show secret access key to see the secret key, and record them somewhere safe before closing the window. You will need to provide these keys when you edit the Access policy of the SQS queue and when setting the AWS Client ID and AWS Client Secret in Cortex XSIAM. If you forget to record the keys and close the window, you will need to generate new keys and repeat this process.

        For more information, see [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
6.  Update the Access policy of your Amazon SQS queue.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> Skip this step if you are using an Assumed Role or Workload Federated Identity for Cortex XSIAM.</p></div>

    1. In the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), select the SQS queue that you created when you configured an Amazon Simple Queue Service (SQS).
    2. Select the Access policy tab, and edit the Access policy code in the editor window to enable the IAM user to perform operations on the Amazon SQS with permissions to `SQS:ChangeMessageVisibility`, `SQS:DeleteMessage`, `SQS:ReceiveMessage`, and `SQS:GetQueueAttributes`. Use this sample code as a guide for defining the `“Sid”: “__receiver_statement”` with the following definitions.
       * `“aws:SourceArn”`: Specify the ARN of the AWS IAM user. You can retrieve the User ARN from the Security credentials tab, which you accessed when you configured access keys for the AWS API user.
       *   `“Resource”`: Leave the automatically generated ARN for the SQS queue that is set in the code, which uses the format `“arn:sns:Region:account-id:topic-name”`.

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong> For more information on granting permissions to publish messages to an SQS queue, see <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html">Granting permissions to publish event notification messages to a destination</a>.</p></div>

           ```
           {
             "Version": "2012-10-17",
             "Statement": [
               {
                 "Effect": "Allow",
                 "Principal": {
                   "Service": "s3.amazonaws.com"
                 },
                 "Action": "SQS:SendMessage",
                 "Resource": "[Leave automatically generated ARN for the SQS queue defined by AWS]",
                 "Condition": {
                   "ArnLike": {
                     "aws:SourceArn": "[ARN of your Amazon S3 bucket]"
                   }
                 }
               },
              {
                 "Sid": "__receiver_statement",
                 "Effect": "Allow",
                 "Principal": {
                   "AWS": "[Add the ARN for the AWS IAM user]"
                 },
                 "Action": [
                   "SQS:ChangeMessageVisibility",
                   "SQS:DeleteMessage",
                   "SQS:ReceiveMessage",
                   "sqs:GetQueueAttributes"
                 ],
                 "Resource": "[Leave automatically generated ARN for the SQS queue defined by AWS]"
               }
             ]
           }
           ```
7. Configure the Amazon S3 collection in Cortex XSIAM.
   1. Navigate to Settings → Data Sources & Integrations.
   2. On the Data Sources & Integrations page, click + Add New, search for Amazon S3, then hover over it and click Add.
   3. Select the authentication method you configured and enter the values relevant for your method:

<table><thead><tr><th width="168.859375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the Role ARN for the Assumed Role you created in AWS.</td></tr><tr><td>Audience</td><td>(Workload Federated Identity only) Specify the OIDC audience value configured in your AWS IAM identity provider trust policy. This value scopes the OIDC token to your specific AWS environment.</td></tr><tr><td>AWS Client ID</td><td>(Access Key only) Specify the Access key ID, which you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>AWS Client Secret</td><td>(Access Key only) Specify the Secret access key you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>External ID</td><td>(STS AssumeRole only) Specify the External ID for the Assumed Role you created in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Generic</strong> to configure your log collection to receive generic logs from Amazon S3, which can include different types of data, such as file and metadata.</td></tr><tr><td>Log Format</td><td><p>Select the log format type as Raw, JSON, CEF, LEEF, Cisco, Corelight, or Beyondtrust Cloud ECS.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note:</strong></p><ul><li>The Vendor and Product defaults to Auto-Detect when the Log Format is set to CEF or LEEF.</li><li>For CEF or LEEF log formats, Cortex XSIAM parses events row by row for Vendor and Product values. Populated row values override any Vendor and Product specified in the Amazon S3 data collector settings. If the row values are blank, Cortex XSIAM falls back to your S3 collector settings; if those are also left blank, both fields default to unknown.</li></ul></div></td></tr><tr><td>Vendor</td><td>(Optional) Specify a particular vendor name for the Amazon S3 generic data collection, which is used in the Amazon S3 XQL dataset <code>&#x3C;Vendor>_&#x3C;Product>_raw</code> that Cortex XSIAM creates as soon as it begins receiving logs.</td></tr><tr><td>Product</td><td>(Optional) Specify a particular product name for the Amazon S3 generic data collection, which is used in the Amazon S3 XQL dataset name <code>&#x3C;Vendor>_&#x3C;Product>_raw</code> that Cortex XSIAM creates as soon as it begins receiving logs.</td></tr><tr><td>Compression</td><td>Select whether the logs are compressed into a gzip file or are uncompressed.</td></tr><tr><td>Multiline Parsing Regex</td><td>(Optional, Raw format only) Enter a regular expression to identify the start of a new log event. Cortex XSIAM assumes each new event start indicates the previous event has ended.</td></tr></tbody></table>

When **Log Format** is set to one of the following, the fields are pre-populated as shown:

| **Log Format**        | **Vendor**  | **Product**          | **Compression** | **Configurable?** |
| --------------------- | ----------- | -------------------- | --------------- | ----------------- |
| Beyondtrust Cloud ECS | Beyondtrust | Privilege Management | Uncompressed    | No                |
| Cisco                 | Cisco       | ASA                  | _N/A_           | No                |
| Corelight             | Corelight   | Zeek                 | _N/A_           | No                |
| Raw or JSON           | AMAZON      | AWS                  | _N/A_           | Yes               |

* Cortex XSIAM supports logs in single-line format or multiline format. For a JSON format, multiline logs are collected automatically when the Log Format is configured as JSON. When configuring a Raw format, you must also define the Multiline Parsing Regex as explained below.

d. Click Test to validate access, and then click **Enable**.

Once events start to come in, a green check mark appears underneath the Amazon S3 configuration with the number of logs received.
