# Create an assumed role

If you do not designate a separate AWS IAM user to provide access to Cortex XSIAM to your logs and to perform API operations, you can create an assumed role in AWS to delegate permissions to a Cortex XSIAM AWS service. This role grants Cortex XSIAM access to your logs. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html).

When setting up any type of Amazon S3 Collector in Cortex XSIAM, these instructions explain setting up an Assumed Role.

{% hint style="info" %}
**Prerequisite**

You need ensure you have an Amazon S3 bucket and Amazon Simple Queue Service (SQS) already configured as it's needed to configure an IAM policy. The S3 bucket and SQS required depends on how you plan to configure your Amazon S3 data source:

* When using a CloudFormation script provided by Cortex XSIAM to configure Amazon S3 with SQS notifications, you'll need to either:
  * Use the out-of-the-box Amazon S3 bucket and Amazon Simple Queue Service (SQS), whose names change according to the Amazon S3 log type you are defining.
  * Create a new S3 bucket and SQS according to your system requirements.
* When configuring data collection from Amazon S3 manually, create a S3 bucket and SQS according to your system requirements.

When creating the S3 bucket and SQS, follow any other relevant instructions provided, for example in the prerequisite section, for the specific type of Amazon S3 data you want to ingest in the relevant topic.
{% endhint %}

1. Log in to the AWS Management Console, and open the IAM console to create a policy in the same region as your AWS account.
   1. In the navigation pane on the left, select Access Management → Policies, and click Create policy.
   2. For the Policy editor, select the JSON tab.
   3.  Copy the following JSON policy and paste it within the editor window.

       The **`<s3-arn>`** and **`<sqs-arn>`** are placeholders. These are filled out using the S3 bucket and SQS that you configured in the prerequisite steps above.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><ul><li>You can retrieve your bucket’s ARN by opening the <a href="https://console.aws.amazon.com/s3/">Amazon S3 Console</a> in a browser window. In the Buckets section, select the bucket, click Copy ARN, and paste the ARN in the field.</li><li>You can retrieve the SQS queue ARN by opening another instance of the AWS Management Console in a browser window, and opening the <a href="https://console.aws.amazon.com/sqs/">Amazon SQS Console</a>, and selecting the Amazon SQS that you created. In the Details section, under ARN, click the copy icon (<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAATCAYAAAB2pebxAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QYcBzsjhEi12QAAAIlJREFUOI1j/P///38GCgETpQYMLkNYsAnWt3YzXLt+i6BmbU11hobqEuwuIcYABgYGhqvXb+J2CQysXjIbp1xoTCqcDTcEmxeQFcIAzAvIAO4dUr2ADDC8Q6wXsLqEEjDEDUEPG4pcoqWpxsDAQCCx4QLoMYhhCK5oxAfg3oE5jRDApo6RGiUbANIcKtiGO7bCAAAAAElFTkSuQmCC" alt="copy-icon.png">)), and paste the ARN in the field.</li></ul></div>

       ```
       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": "s3:GetObject",
                   "Resource": "<s3-arn>/*"
               },
               {
                   "Effect": "Allow",
                    "Action": [
                       "sqs:ReceiveMessage",
                       "sqs:DeleteMessage",
                       "sqs:ChangeMessageVisibility"
                   ],
                   "Resource": "<sqs-arn>"
               }
           ]
       }
       ```
   4. Click Next.
   5. Review and create the policy.
2.  Create a role for Cortex XSIAM in the IAM console of the AWS Management Console.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For more information, see the <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html">AWS instructions</a>.</p></div>

    1. In the navigation pane on the left, select Access Management → Roles, and click Create role.
    2.  Select trusted entity, and use the following values and options when creating the role:

        * Trusted entity type: Select Custom trust policy.
        * Custom trust policy: On the right pane, configure the following settings.
          * Under Edit statement → Read or write, verify the AssumeRole is selected.
          *   Add a principle by clicking Add and setting the following:

              * Principal type: Select AWS account and root user.
              * ARN: Replace (Account) with the Account ID 006742885340. When using a Cortex XSIAM FedRAMP environment, specify the Account ID as 685269782068.

              When you are finished, click Add principal.
          *   Add a condition for an External ID by clicking Add and setting the following:

              * Condition key: Select sts:ExternalId.
              * Qualifier: Select Default.
              * Operator: Select StringEquals.
              * Value: Enter the value of the External ID, a unique alphanumeric string, by generating a secure UUIDv4 using an [Online UUID Generator](https://www.uuidgenerator.net/version4). Copy the External ID as you will use this when configuring the Amazon S3 Collector in Cortex XSIAM.

              <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FNr3QLuWbBFvp1f8hglgI%2Fadd-condition.png?alt=media&#x26;token=961565fa-9424-4daf-81cf-15afdfa7ca6e" alt=""><figcaption></figcaption></figure>

              When you are finished, click Add condition.

        <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FFmCPWQgC4Parmvsa71Lr%2Fselect-trusted-entity.png?alt=media&#x26;token=2902a1c8-f521-47dc-9cc9-9e790ce1a2af" alt=""><figcaption></figcaption></figure>
    3.  Click Next and add permissions by selecting the policy you created.

        <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FL8qI8UImsTYwK48NqjKC%2Fadd-permissions.png?alt=media&#x26;token=b6a6adb9-cf6c-4343-b9f0-2d569c2137d3" alt=""><figcaption></figcaption></figure>
3.  Click Next to name, review, and create.

    * Role name: Specify a name for the new role, and click Create role.

    <figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fo4Eomsck1rOFolzX8xsy%2Fname-review-create.png?alt=media&#x26;token=fd5866ff-3ed5-4799-b36b-10e99711a2fa" alt=""><figcaption></figcaption></figure>
4. Copy the Policy ARN and Role ARN for future use by opening the policy and role that you created.
5.  Continue with the task for the applicable Amazon S3 logs you want to configure.

    The following types of logs are available.

    * [Ingest network flow logs from Amazon S3](ingest-network-flow-logs-from-amazon-s3).
    * [Ingest network Route 53 logs from Amazon S3](ingest-network-route-53-logs-from-amazon-s3)
    * [Ingest audit logs from AWS Cloud Trail](ingest-audit-logs-from-aws-cloudtrail).
    * [Ingest generic logs from Amazon S3](ingest-generic-logs-from-amazon-s3).
