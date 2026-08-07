# Ingest audit logs from AWS CloudTrail

You can forward audit logs for the relative service to Cortex Cloud from AWS CloudTrail.

To receive audit logs from Amazon Simple Storage Service (Amazon S3) via AWS CloudTrail, you must first configure data collection from Amazon S3. You can then configure the Data Sources & Integrations settings in Cortex Cloud for Amazon S3. After you set up collection integration, Cortex Cloud begins receiving new logs and data from the source.

We do not recommend ingestion of data from an AWS commercial environment into a FedRAMP-certified Cortex Cloud tenant. However, if you must do so, contact Customer Support for assistance.

{% hint style="info" %}
**Note**

For more information on configuring data collection from Amazon S3 using AWS CloudTrail, see the [AWS CloudTrail Documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html).
{% endhint %}

When Cortex Cloud begins receiving logs, the app automatically creates an Amazon S3 Cortex Query Language (XQL) dataset (`aws_s3_raw`). This enables you to search the logs with XQL Search using the dataset. For example queries, refer to the in-app XQL Library.

For enhanced cloud protection, you can also configure Cortex Cloud to stitch Amazon S3 audit logs with other Cortex Cloud authentication stories across all cloud providers using the same format, which you can query with XQL Search using the `cloud_audit_logs` dataset. Cortex Cloud can also generate Cortex Cloud issues (Analytics, IOC, BIOC, and Correlation Rules), when relevant, from Amazon S3 logs. While Correlation Rules issues are generated on non-normalized and normalized logs, Analytics, IOC, and BIOC issues are only generated on normalized logs.

Enhanced cloud protection provides the following:

* Normalization of cloud logs
* Cloud logs stitching
* Enrichment with cloud data
* Detection based on cloud analytics
* Cloud-tailored investigations

**Prerequisite Steps**

Be sure you do the following tasks before you begin configuring data collection from Amazon S3 via AWS CloudTrail.

* Ensure that you have the proper permissions to access AWS CloudTrail and have the necessary permissions to create audit logs. The following permissions in AWS are the minimum requirements for an Amazon S3 bucket and Amazon Simple Queue Service (SQS).
  * **Amazon S3 bucket**: `GetObject`
  * **SQS**: `ChangeMessageVisibility`, `ReceiveMessage`, and `DeleteMessage`.
* Determine how you want to provide access to Cortex Cloud to your logs and to perform API operations. You have the following options:
  * Use Workload Federated Identity to allow Cortex Cloud's dedicated log collector service account to assume an IAM role in your AWS environment without storing any long-lived credentials. This is the **Workload Federated Identity** option described in the Amazon S3 collection configuration. This is the recommended option when your log collector is deployed as a Cortex-managed cloud service.
  * Designate an AWS IAM user, where you will need to know the Account ID for the user and have the relevant permissions to create an access key/id for the relevant IAM user. This is the default option as explained in Configure the Amazon S3 collection by selecting Access Key.
  * Create an assumed role in AWS to delegate permissions to a Cortex Cloud AWS service. This role grants Cortex Cloud access to your flow logs. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html). This is the Assumed Role option described in the Amazon S3 collection configuration. To collect Amazon S3 logs that use server-side encryption (SSE), the user role must have an IAM policy that states that Cortex Cloud has kms:Decrypt permissions. With this permission, Amazon S3 automatically detects if a bucket is encrypted and decrypts it. If you want to collect encrypted logs from different accounts, you must have the decrypt permissions for the user role also in the key policy for the master account Key Management Service (KMS). For more information, see [Allowing users in other accounts to use a KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).
* If using **Workload Federated Identity**, ensure you have permissions to create an AWS IAM Identity Provider and an IAM role with a trust policy in your AWS account. You will need the Cortex Cloud service account identifier (provided in the Cortex Cloud UI after saving the configuration) to configure the trust relationship.

To configure Cortex Cloud to receive audit logs from Amazon S3 via AWS Cloudtrail:

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/).
2. From the menu bar, ensure that you have selected the correct region for your configuration.
3.  Configure an AWS CloudTrail trail with audit logs.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><ul><li>For more information on creating an AWS CloudTrail trail, see <a href="https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html">Create a trail</a>.</li><li>If you already have an Amazon S3 bucket configured with AWS CloudTrail audit logs, skip this step and go to Configure an Amazon Simple Queue Service (SQS).</li></ul></div>

    1. Open the [CloudTrail Console](https://console.aws.amazon.com/cloudtrail/), and click Create trail.
    2.  Configure the following settings for your CloudTrail trail, where the default settings should be configured unless otherwise indicated.

        * Trail name: Specify a descriptive name for your CloudTrail trail.
        *   Storage location: Select Create new S3 bucket to configure a new Amazon S3 bucket, and specify a unique name in the Trail log bucket and folder field, or select Use existing S3 bucket and Browse to the S3 bucket you already created. If you select an existing Amazon S3 bucket, the bucket policy must grant CloudTrail permission to write to it. For information about manually editing the bucket policy, see [Amazon S3 Bucket Policy for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/create-s3-bucket-policy-for-cloudtrail.html).

            <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>It is your organization's responsibility to define a retention policy for your Amazon S3 bucket by creating a Lifecycle rule in the Management tab. We recommend setting the retention policy to at least 7 days to ensure that the data is retrieved under all circumstances.</p></div>
        * Customer managed AWS KMS key: You can either select a New key and specify the AWS KMS alias, or select an Existing key, and select the AWS KMS alias. The KMS key and S3 bucket must be in the same region.
        * SNS notification delivery: (Optional) If you want to be notified whenever CloudTrail publishes a new log to your Amazon S3 bucket, click Enabled. Amazon Simple Notification Service (Amazon SNS) manages these notifications, which are sent for every log file delivery to your S3 bucket, as opposed to every event. When you enable this option, you can either Create a new SNS topic by selecting New and the SNS topic is displayed in the field, or use an Existing topic and select the SNS topic. For more information, see [Configure SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/configure-sns-notifications-for-cloudtrail.html).

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The CloudWatch Logs - optional settings are not supported and should be left disabled.</p></div>
    3. Click **Next**, and configure the following Choose log events settings.
       * Event type: Leave the default Management events checkbox selected to capture audit logs. Depending on your system requirements, you can also select Data events to log the resource operations performed on or within a resource, or Insights events to identify unusual activity, errors, or user behavior in your account. Based on your selection, additional fields are displayed on the screen to configure under section headings with the same name as the event type.
       *   Management events section: Configure the following settings.

           -API activity: For Management events, select the API activities you want to log. By default, the Read and Write activities are logged.

           -Exclude AWS KMS events: (Optional) If you want to filter AWS Key Management Service (AWS KMS) events out of your trail, select the checkbox. By default, all AWS KMS events are included.
       * Data events section: (Optional) This section is displayed when you configure the Event type to include Data events, which relate to resource operations performed on or within a resource, such as reading and writing to a S3 bucket. For more information on configuring these optional settings in AWS CloudTrail, see [Creating a trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html).
       * Insights events section: (Optional) This section is displayed when you configure the Event type to include Insight events, which relate to unusual activities, errors, or user behavior on your account. For more information on configuring these optional settings in AWS CloudTrail, see [Creating a trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html).
    4. Click Next.
    5.  In the Review and create page, look over the trail configurations settings that you have configured and if they are correct, click Create trail. If you need to make a change, click Edit beside the particular step that you want to update.

        The new trail is listed in the Trails page, which lists the trails in your account from all Regions. It can take up to 15 minutes for CloudTrail to begin publishing log files. You can see the log files in the S3 bucket that you specified. For more information, see [Creating a trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html).
4.  Configure an Amazon Simple Queue Service (SQS).

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Ensure that you create your Amazon S3 bucket and Amazon SQS queue in the same region.</p></div>

    1. In the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), click Create Queue.
    2. Configure the following settings, where the default settings should be configured unless otherwise indicated.
       * Type: Select Standard queue (default).
       * Name: Specify a descriptive name for your SQS queue.
       * Configuration section: Leave the default settings for the various fields.
       *   Access policy → Choose method: Select Advanced and update the Access policy code in the editor window to enable your Amazon S3 bucket to publish event notification messages to your SQS queue. Use this sample code as a guide for defining the `“Statement”` with the following definitions:

           -**`“Resource”`**: Leave the automatically generated ARN for the SQS queue that is set in the code, which uses the format `“arn:sqs:region:account-id:queue-name”`.

           You can retrieve your bucket’s ARN by opening the [Amazon S3 Console](https://console.aws.amazon.com/s3/) in a browser window. In the Buckets section, select the bucket that you created for collecting the AWS CloudTrail logs, click Copy ARN, and paste the ARN in the field.

           ![bucket-copy-arn.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/GD6sG6FlxDWxAn13_eZuUQ/resources/9VZLtdPYotIjTFCpZQf9vg-GD6sG6FlxDWxAn13_eZuUQ/content?v=0a86423f550de7ed\&Ft-Calling-App=ft/turnkey-portal)

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For more information on granting permissions to publish messages to an SQS queue, see <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html">Granting permissions to publish event notification messages to a destination</a>.</p></div>

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
             ]
           }
           ```
       * Dead-letter queue section: We recommend that you configure a queue for sending undeliverable messages by selecting Enabled, and then in the Choose queue field selecting the queue to send the messages. You may need to create a new queue for this, if you do not already have one set up. For more information, see [Amazon SQS dead-letter queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html).
    3.  Click Create queue.

        Once the SQS is created, a message indicating that the queue was successfully configured is displayed at the top of the page.
5. Configure an event notification to your Amazon SQS whenever a file is written to your Amazon S3 bucket.
   1. Open the [Amazon S3 Console](https://console.aws.amazon.com/s3/) and in the Properties tab of your Amazon S3 bucket, scroll down to the Event notifications section, and click Create event notification.
   2. Configure the following settings.
      * Event name: Specify a descriptive name for your event notification containing up to 255 characters.
      * Prefix: Do not set a prefix as the Amazon S3 bucket is meant to be a dedicated bucket for collecting audit logs.
      * Event types: Select All object create events for the type of event notifications that you want to receive.
      * Destination: Select SQS queue to send notifications to an SQS queue to be read by a server.
      *   Specify SQS queue: You can either select Choose from your SQS queues and then select the SQS queue, or select Enter SQS queue ARN and specify the ARN in the SQS queue field.

          You can retrieve your SQS queue ARN by opening another instance of the AWS Management Console in a browser window, and opening the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), and selecting the Amazon SQS that you created. In the Details section, under ARN, click the copy icon (![copy-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAATCAYAAAB2pebxAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QYcBzsjhEi12QAAAIlJREFUOI1j/P///38GCgETpQYMLkNYsAnWt3YzXLt+i6BmbU11hobqEuwuIcYABgYGhqvXb+J2CQysXjIbp1xoTCqcDTcEmxeQFcIAzAvIAO4dUr2ADDC8Q6wXsLqEEjDEDUEPG4pcoqWpxsDAQCCx4QLoMYhhCK5oxAfg3oE5jRDApo6RGiUbANIcKtiGO7bCAAAAAElFTkSuQmCC)), and paste the ARN in the field.

          ![sqs-arn2.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/GD6sG6FlxDWxAn13_eZuUQ/resources/Uwrw8tPTiwt~g2r7GVJ4oQ-GD6sG6FlxDWxAn13_eZuUQ/content?v=ae47fe6bece0aed5\&Ft-Calling-App=ft/turnkey-portal)
   3.  Click **Save changes**.

       Once the event notification is created, a message indicating that the event notification was successfully created is displayed at the top of the page.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If your receive an error when trying to save your changes, you should ensure that the permissions are set up correctly.</p></div>
6.  Configure access keys for the AWS IAM user that Cortex Cloud uses for API operations.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><ul><li>It your organization's responsibility to ensure that the user who performs this task of creating the access key is designated with the relevant permissions. Otherwise, this can cause the process to fail with errors.</li><li>Skip this step if you are using an <strong>Assumed Role</strong> or <strong>Workload Federated Identity</strong> for Cortex Cloud.</li></ul></div>

    1. Open the [AWS IAM Console](https://console.aws.amazon.com/iam/), and in the navigation pane, select Access management → Users.
    2. Select the User name of the AWS IAM user.
    3. Select the Security credentials tab, scroll down to the Access keys section, and click Create access key.
    4.  Click the copy icon next to the Access key ID and Secret access key keys, where you must click Show secret access key to see the secret key and record them somewhere safe before closing the window. You will need to provide these keys when you edit the Access policy of the SQS queue and when setting the AWS Client ID and AWS Client Secret in Cortex Cloud. If you forget to record the keys and close the window, you will need to generate new keys and repeat this process.

        <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For more information, see <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html">Managing access keys for IAM users</a>.</p></div>
7.  Update the Access policy of your Amazon SQS queue.

    Skip this step if you are using an **Assumed Role** or **Workload Federated Identity** for Cortex Cloud.

    1. In the [Amazon SQS Console](https://console.aws.amazon.com/sqs/), select the SQS queue that you created in Configure an Amazon Simple Queue Service (SQS).
    2. Select the Access policy tab, and Edit the Access policy code in the editor window to enable the IAM user to perform operations on the Amazon SQS with permissions to `SQS:ChangeMessageVisibility`, `SQS:DeleteMessage`, and `SQS:ReceiveMessage`. Use this sample code as a guide for defining the `“Sid”: “__receiver_statement”` with the following definitions:
       * **`“aws:SourceArn”`**: Specify the ARN of the AWS IAM user. You can retrieve the User ARN from the Security credentials tab, which you accessed when configuring access keys for the AWS API user.
       *   **`“Resource”`**: Leave the automatically generated ARN for the SQS queue that is set in the code, which uses the format `“arn:sqs:region:account-id:queue-name”`.

           <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For more information on granting permissions to publish messages to an SQS queue, see <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html">Granting permissions to publish event notification messages to a destination</a>.</p></div>

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
8. Configure the Amazon S3 collection in Cortex Cloud.
   1. Navigate to **Settings → Data Sources & Integrations**.
   2. On the **Data Sources & Integrations** page, click **+ Add New**, search for Amazon S3, then hover over it and click **Add**.
   3. Select the authentication method you configured and enter the following values:

{% tabs %}
{% tab title="Workload Federated Identity" %}
Delegates permissions to a Cortex Cloud AWS service using an IAM assumed role. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

<table><thead><tr><th width="169.71484375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the ARN of the IAM role that Cortex Cloud's log collector will assume. This role must have a trust policy that allows Cortex Cloud's service account to assume it.</td></tr><tr><td>Audience</td><td>Specify the OIDC audience value configured in your AWS IAM identity provider trust policy. This value scopes the OIDC token to your specific AWS environment.</td></tr><tr><td>Log Type</td><td>Select <strong>Audit Logs</strong> to configure your log collection to receive audit logs from Amazon S3 via AWS CloudTrail.</td></tr><tr><td>Use audit logs in analytics</td><td>If selected, Cortex Cloud stitches Amazon S3 audit logs with other Cortex Cloud authentication stories across all cloud providers using the same format, which you can query with XQL Search using the <code>cloud_audit_logs</code> dataset.</td></tr></tbody></table>

Click **Copy Identifier** to copy the Cortex Cloud service account identifier. Add this identifier to the trust policy of the IAM role in AWS to authorize Cortex Cloud's log collector to assume the role.
{% endtab %}

{% tab title="Access Key" %}
Uses a designated AWS IAM user's static access key and secret to authenticate.

<table><thead><tr><th width="188.20703125">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>AWS Client ID</td><td>Specify the Access key ID, which you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>AWS Client Secret</td><td>Specify the Secret access key you received when you configured access keys for the AWS IAM user in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Audit Logs</strong> to configure your log collection to receive audit logs from Amazon S3 via AWS CloudTrail.</td></tr><tr><td>Use audit logs in analytics</td><td>If selected, Cortex Cloud stitches Amazon S3 audit logs with other Cortex Cloud authentication stories across all cloud providers using the same format, which you can query with XQL Search using the <code>cloud_audit_logs</code> dataset.</td></tr></tbody></table>
{% endtab %}

{% tab title="Assumed Role" %}
Delegates permissions to a Cortex Cloud AWS service using an IAM assumed role. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

<table><thead><tr><th width="168.859375">Field</th><th>Input</th></tr></thead><tbody><tr><td>SQS URL</td><td>Specify the <strong>SQS URL</strong>, which is the URL of the Amazon SQS that you configured in the AWS Management Console.</td></tr><tr><td>Name</td><td>Specify a descriptive name for your log collection configuration.</td></tr><tr><td>Role ARN</td><td>Specify the Role ARN for the Assumed Role you created in AWS.</td></tr><tr><td>External ID</td><td>Specify the External ID for the Assumed Role you created in AWS.</td></tr><tr><td>Log Type</td><td>Select <strong>Audit Logs</strong> to configure your log collection to receive audit logs from Amazon S3 via AWS CloudTrail.</td></tr><tr><td>Use audit logs in analytics</td><td>If selected, Cortex Cloud stitches Amazon S3 audit logs with other Cortex Cloud authentication stories across all cloud providers using the same format, which you can query with XQL Search using the <code>cloud_audit_logs</code> dataset.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

d. Click Test to validate access, and then click **Enable**.

Once events start to come in, a green check mark appears underneath the Amazon S3 configuration with the number of logs received.
