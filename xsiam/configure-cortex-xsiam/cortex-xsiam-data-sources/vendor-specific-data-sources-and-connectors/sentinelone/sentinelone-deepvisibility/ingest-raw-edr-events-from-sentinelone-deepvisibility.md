---
description: Ingest SentinelOne DeepVisibility raw EDR events into Cortex XSIAM.
---

# Ingest raw EDR events from SentinelOne DeepVisibility

Cortex XSIAM enables ingestion of raw EDR event data from SentinelOne DeepVisibility, streamed via Cloud Funnel to Amazon S3. In addition to all standard SIEM capabilities, this integration unlocks some advanced Cortex XSIAM features, enabling comprehensive analysis of data from all sources, enhanced detection and response, and deeper visibility into SentinelOne data.

Key benefits include:

* Querying all raw event data received from SentinelOne using XQL.
* Querying critical modeled and unified EDR data via the `xdr_data` dataset.
* Enriching case and issue investigations with relevant context.
* Grouping issues with issues from other sources to accelerate the scoping process of cases, and to cut investigation time.
* Leveraging the data for analytics-based detection.
* Utilizing the data for rule-based detection, including correlation rules, BIOC, and IOC.
* Leveraging the data within playbooks for case response.

When Cortex XSIAM begins receiving EDR events from SentinelOne, it automatically creates a new dataset labeled `sentinelone_deep_visibility_raw`, allowing you to query all SentinelOne events using XQL. For example XQL queries, refer to the in-app XQL Library.

In addition, Cortex XSIAM parses and maps critical data into the `xdr_data` dataset and XDM data model, enabling unified querying and investigation across all supported EDR vendors' data and unlocking key benefits like stitching and advanced analytics. While mapped data from all supported EDR vendors, including SentinelOne DeepVisibility, will be available in the `xdr_data` dataset, it's important to note that third-party EDR data present some limitations.

Third-party agents, including SentinelOne, typically provide less data compared to our native agents, and do not include the same level of optimization for causality analysis and cloud-based analytics. Furthermore, external EDR rate limits and filters might restrict the availability of critical data required for comprehensive analytics. As a result, only a subset of our analytics-based detectors will function with third-party EDR data.

We are continuously enhancing our support and using advanced techniques to enrich missing third-party data, while somehow replicating some proprietary functionalities available with our agents. This approach maximizes value for our customers using third-party EDRs within existing constraints. However, it’s important to recognize that the level of comprehensiveness achieved with our native agents cannot be matched, as much of the logic happens on the agent itself. These capabilities are unique, and are not found in typical SIEMs. Many of them, along with their underlying logic, are patented by Palo Alto Networks. Therefore, they should be regarded as added value beyond standard SIEM functionalities for customers who are not using our agents.

* The SentinelOne DeepVisibility logs that will be collected by your dedicated Amazon S3 bucket must adhere to the following guidelines:
  * Each log file must use the 1 log per line format as multi-line format is not supported.
  * The log format must be compressed as gzip or uncompressed.
  * For best performance, we recommend limiting each file size to up to 50 MB (compressed).
* The minimum AWS permissions required for an Amazon S3 bucket and Amazon Simple Queue Service (SQS) are:
  * **Amazon S3 bucket**: `GetObject`
  * **SQS**: `ChangeMessageVisibility`, `ReceiveMessage`, and `DeleteMessage`
* Determine how you want to provide access to Cortex XSIAM to your logs and to perform API operations. You have the following options:
  * Designate an AWS IAM user, where you will need to know the Account ID for the user and have the relevant permissions to create an access key/id for the relevant IAM user. If you do not have a designated AWS IAM user configured yet, instructions for this are included in the following procedures.
  *   Create an assumed role in AWS to delegate permissions to a Cortex XSIAM AWS service. This role grants Cortex XSIAM access to your flow logs. This is the Assumed Role option mentioned later in the procedures that follow. To create an assumed role for Cortex XSIAM, see [Create an assumed role](https://docs-cortex.paloaltonetworks.com/r/5CAbsl8idaK8R43ZLhoTOw/VoyBaGgwFQAaZsR2JlCQfQ).

      For more information about assumed roles, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).
* To collect Amazon S3 logs that use server-side encryption (SSE), the user role must have an IAM policy that states that Cortex XSIAM has kms:Decrypt permissions. With this permission, Amazon S3 automatically detects if a bucket is encrypted and decrypts it. If you want to collect encrypted logs from different accounts, you must have the decrypt permissions for the user role also in the key policy for the master account Key Management Service (KMS). For more information, see [Allowing users in other accounts to use a KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).

### **Task 1: Configure an Amazon S3 bucket**

#### Task A: Create a dedicated Amazon S3 bucket to store SentinelOne DeepVisibility EDR data

This step provides general guidelines. For more information, see [Creating a bucket using the Amazon S3 Console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html).

It is your responsibility to define a retention policy for your Amazon S3 bucket by creating a Lifecycle rule on the Management tab. We recommend setting the retention policy to at least 7 days to ensure that the data is retrieved under all circumstances.

1. Log in to the AWS Management Console and navigate to the S3 Service.
2. Create a new S3 bucket:
   1. Click Create bucket.
   2. For Bucket Name, enter a unique name for the bucket (for example, `xsiam-s1-edr-data`).
   3. Choose an appropriate AWS Region.
   4. Set Block all public access to Enabled.
   5. Click Create bucket.
3. Set up the Bucket policy:
   1. Click the Permissions tab of your new bucket.
   2.  Under Bucket policy, click Edit and add the following policy to allow SentinelOne DeepVisibility to write data there.

       Replace `your-sentinelone-account-id` with the relevant value for your environment; replace `xsiam-s1-edr-data` with the name of your new bucket.

       ```
       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Effect": "Allow",
                   "Principal": {
                       "AWS": "your-sentinelone-account-id"
                   },
                   "Action": "s3:PutObject",
                   "Resource": "arn:aws:s3:::xsiam-s1-edr-data/*"
               }
           ]
       }
       ```

#### Task B: Configure an Amazon Simple Queue Service (SQS) and grant it permission to receive messages from S3

{% hint style="info" %}
Ensure that you create your Amazon S3 bucket and Amazon SQS queue in the same region.
{% endhint %}

1. In the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), click Create Queue.
2. Configure the following settings, where the default settings should be configured unless otherwise indicated.
   * Type: Select Standard queue (default).
   * Name: Specify a descriptive name for your SQS queue.
   * Configuration section: Keep the default settings for the various fields.
   *   Access policy → Choose method: Select Advanced and update the Access policy code in the editor window to enable your Amazon S3 bucket to publish event notification messages to your SQS queue. Use this sample code as a guide for defining the `“Statement”` with the following definitions.

       **`“Resource”`**: Keep the automatically generated ARN for the SQS queue that is set in the code, which uses the format `“arn:sns:Region:account-id:topic-name”`.

       You can retrieve your bucket’s ARN by opening the [Amazon S3 Console](https://console.aws.amazon.com/s3/) in a browser window. In the Buckets section, select the bucket that you created for collecting the Amazon S3 flow logs, click Copy ARN, and paste the ARN in the field.

       [![bucket-copy-arn.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/6WNDrnSEbyRhjXn56dpdLA-5CAbsl8idaK8R43ZLhoTOw/content?v=0a86423f550de7ed\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/6WNDrnSEbyRhjXn56dpdLA-5CAbsl8idaK8R43ZLhoTOw)

       For more information on granting permissions to publish messages to an SQS queue, see [Granting permissions to publish event notification messages to a destination](https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html).

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

    When the SQS is created, a message indicating that the queue was successfully configured is displayed at the top of the page.

#### Task C: Configure an event notification to your Amazon SQS whenever a file is written to your Amazon S3 bucket

1. Open the [Amazon S3 Console](https://console.aws.amazon.com/s3/) and in the Properties tab of your Amazon S3 bucket, scroll down to the Event notifications section, and click Create event notification.
2. Configure the following settings:
   * Event name: Specify a descriptive name for your event notification containing up to 255 characters.
   * Prefix: Do not set a prefix, because the Amazon S3 bucket is meant to be a dedicated bucket for collecting only network flow logs.
   * Event types: Select All object create events for the type of event notifications that you want to receive.
   * Destination: Select SQS queue to send notifications to an SQS queue to be read by a server.
   *   Specify SQS queue: You can either select Choose from your SQS queues and then select the SQS queue, or select Enter SQS queue ARN and specify the ARN in the SQS queue field.

       You can retrieve your SQS queue ARN by opening another instance of the AWS Management Console in a browser window, opening the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), and selecting the Amazon SQS that you created. In the Details section, under ARN, click the copy icon ([![copy-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAATCAYAAAB2pebxAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QYcBzsjhEi12QAAAIlJREFUOI1j/P///38GCgETpQYMLkNYsAnWt3YzXLt+i6BmbU11hobqEuwuIcYABgYGhqvXb+J2CQysXjIbp1xoTCqcDTcEmxeQFcIAzAvIAO4dUr2ADDC8Q6wXsLqEEjDEDUEPG4pcoqWpxsDAQCCx4QLoMYhhCK5oxAfg3oE5jRDApo6RGiUbANIcKtiGO7bCAAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/zZbioenAsJylLzQVFAgpBg-5CAbsl8idaK8R43ZLhoTOw))), and paste the ARN in the field.

       [![sqs-arn2.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/eYfeDS1_a6RDwMUNv0iHvA-5CAbsl8idaK8R43ZLhoTOw/content?v=ae47fe6bece0aed5\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/eYfeDS1_a6RDwMUNv0iHvA-5CAbsl8idaK8R43ZLhoTOw)
3.  Click Save changes.

    When the event notification is created, a message indicating that the event notification was successfully created is displayed at the top of the page.

    If you receive an error when trying to save your changes, check that the permissions are set up correctly, and fix them if necessary.

Task D: Configure authentication\authorization if you have not done so yet

For **Assumed Role**, follow these instructions: [Create an assumed role](https://docs-cortex.paloaltonetworks.com/r/5CAbsl8idaK8R43ZLhoTOw/VoyBaGgwFQAaZsR2JlCQfQ), and then return to this page to [Configure SentinelOne DeepVisibility](https://docs-cortex.paloaltonetworks.com/r/5CAbsl8idaK8R43ZLhoTOw/WnhkcnR1li6SZWdc8TApJQ?section=UUID-cb7d2015-e6df-5be3-ba53-b4d2090fd3e4_section-idm234481154153413).

For **IAM access key**:

1. Create an IAM Policy that grants permissions for SQS and S3:
   1. In the AWS Console, navigate to the IAM service, and click Policies.
   2. Click Create policy.
   3. Select the JSON policy editor.
   4.  Use this sample code as a guide for defining the “Statement” with the following definitions:

       ```
       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Sid": "S3ReadAccess",
                   "Effect": "Allow",
                   "Action": [
                       "s3:GetObject",
                       "s3:ListBucket"
                   ],
                   "Resource": [
                       "[ARN for the S3 Bucket Name defined by AWS]", #example: "arn:aws:s3:::bucketname/xsiam-s1-edr-data/"
                       "[ARN for the S3 Bucket path defined by AWS]" #example: "arn:aws:s3:::bucketname/xsiam-s1-edr-data/*"
                   ]
               },
               {
                   "Sid": "SQSReceiveAccess",
                   "Effect": "Allow",
                   "Action": [
                       "sqs:ReceiveMessage",
                       "sqs:GetQueueAttributes"
                   ],
                   "Resource": "[ARN for the SQS queue defined by AWS]"
               }
           ]
       }
       ```
   5. Click Next.
   6. For Policy name, enter a name.
   7. Click Create policy.
2. Create an IAM User:
   1. In the AWS Console, navigate to the IAM service, and click Users.
   2. Click Create user.
   3. For User name, enter a name (for example, `cortex-xsiam-s3`).
   4. Attach the IAM Policy that you created in Step 1.
   5. Click Next.
   6. Click Create user.
3.  Configure access keys for the AWS IAM User:

    It is the responsibility of your organization to ensure that the user who creates the access key is assigned the relevant permissions. Otherwise, this can cause the process to fail with errors.

    1. Open the [AWS IAM Console](https://console.aws.amazon.com/iam/), and in the navigation pane, select Access management → Users.
    2. Select the User name of the AWS IAM user.
    3. Select the Security credentials tab, scroll down to the Access keys section, and click Create access key.
    4.  Click the copy icon next to the Access key ID and Secret access key keys, where you must click Show secret access key to see the secret key, and save a copy of them somewhere safe before closing the window. You will need to provide these keys when you edit the Access policy of the SQS queue, and when setting the AWS Client ID and AWS Client Secret in Cortex XSIAM. If you forget to record the keys and close the window, you will need to generate new keys and repeat this process.

        For more information, see [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
4. Update the Access policy of your Amazon SQS queue:
   1. In the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), select the SQS queue that you created when you configured an Amazon Simple Queue Service (SQS).
   2. Select the Access policy tab, and click Edit to edit the Access policy code in the editor window, to enable the IAM user to perform operations on the Amazon SQS with the permissions `SQS:ChangeMessageVisibility`, `SQS:DeleteMessage`, and `SQS:ReceiveMessage`. Use this sample code as a guide for defining the `“Sid”: “__receiver_statement”` with the following definitions.
      * `“aws:SourceArn”`: Specify the ARN of the AWS IAM user. You can retrieve the User ARN from the Security credentials tab, which you accessed when you configured access keys for the AWS API user.
      *   `“Resource”`: Keep the automatically generated ARN for the SQS queue that is set in the code, which uses the format `“arn:sns:Region:account-id:topic-name”`.

          For more information on granting permissions to publish messages to an SQS queue, see [Granting permissions to publish event notification messages to a destination](https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html).

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
                  "SQS:ReceiveMessage"
                ],
                "Resource": "[Leave automatically generated ARN for the SQS queue defined by AWS]"
              }
            ]
          }
          ```
   3. Click Save.

### **Task 2: Configure SentinelOne DeepVisibility**

1. In SentinelOne DeepVisibility, select Configure → Policy & Settings and in the Singularity Data Lake section, click Cloud Funnel.
2. For Cloud Provider, select AWS (Amazon Web Services).
3. For S3 Bucket Name, enter the name of the Amazon S3 bucket that you created for SentinelOne DeepVisibility log ingestion.
4. For Telemetry Streaming, select Enable.
5. In the Query Filters box, create a query that includes the agents that should send data to the S3 bucket.
6. To validate the query, click Validate.
7. For Fields to include, ensure that all fields are selected.
8. Click Save.

### Task 3: Configure ingestion into Cortex XSIAM

1. Navigate to Settings → Data Sources & Integrations.
2. On the Data Sources & Integrations page, click + Add New, search for **`SentinelOne - Deep Visibility`**, then hover over it and click Add.
3. Use the toggle to select either Access Key or Assumed Role.
4. Set these parameters, depending on your choice in the previous step:
   * For the Access Key option:
     * Name: Specify a descriptive name for your log collection configuration. This name must be unique in your environment.
     * SQS URL: Specify the SQS URL that you received for the AWS S3 queue when you configured the Amazon Simple Queue Service (SQS), as explained above.
     * AWS Client ID: Specify the Client ID that you received when you configured the AWS IAM user, as explained above.
     * AWS Client Secret: Specify the Secret that you received when you configured the AWS IAM user, as explained above.
   * For the Assumed Role option:
     * Name: Specify a descriptive name for your log collection configuration. This name must be unique in your environment.
     * SQS URL: Specify the SQS URL that you received for the AWS S3 queue when you configured the Amazon Simple Queue Service (SQS), as explained above.
     * Role ARN: Specify the role ARN that you received when you created the assumed role.
     * External Id: Specify the External ID that you received when you created the assumed role.
5.  Click Test to validate access, and then click Enable.

    After events start to come in, a green check mark appears below the SentinelOne - DeepVisibility configuration, along with the amount of data received.
