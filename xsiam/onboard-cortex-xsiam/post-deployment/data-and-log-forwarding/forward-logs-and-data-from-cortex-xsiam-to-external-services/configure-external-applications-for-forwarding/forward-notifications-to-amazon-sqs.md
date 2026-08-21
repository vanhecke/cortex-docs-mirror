# Forward notifications to Amazon SQS

### Create the SQS queue

Log in to your AWS Management Console and create a new **Standard SQS queue**.

### Configure egress in Cortex Gateway

Before forwarding cases or issues to Amazon SQS, you need to configure egress. Only a user with Account Admin or Instance Admin permissions can configure egress.

To configure egress, to enter the queue name. For example, if the full URL is https://sqs.region.amazonaws.com/account-id/queue-name, enter only `queue-name`.

1. In the Cortex Gateway, go to **Permission Management** → **Egress Configurations** → **Path**.
2. Select the account name and tenant.
3. In the Flow field, select **External storage: AWS SQS**.
4. Enter the exact \<queue\_name>. For example, `my-example-queue`. Note that the path does not include HTTP or HTTPS.
5. Add the configuration.

### Generate the authorized party ID

1. In Cortex XSIAM, go to **Settings** → **Configurations** → **Integrations** → **External Applications** → **Add Application** and select **Amazon SQS**.
2. Enter the queue URL from Amazon SQS. Use the URL format rather than the ARN for this specific field.
3. Click **Verify**. If egress has not been configured in the Cortex Gateway, verification will fail and a message will display that the endpoint does not match any approved routes.
4. After verification is successful, an authorized party ID is generated. Copy this ID for your AWS configuration.
5. Leave this page open to complete the application configuration.

### Configure the IAM role and permissions in AWS

Cortex XSIAM needs permission to assume a role in your account.

You can authenticate using either an IAM role or IAM access keys.

* **IAM role**:
  *   In AWS, go to **IAM** → **Roles** → **Create role**, select Custom trust policy, and enter the Trusted Entity JSON, replacing the sub condition with your Authorized party ID. The following is an example:

      ```programlisting
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Principal": {
              "Federated": "accounts.google.com"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
              "StringEquals": {
                "accounts.google.com:sub": "<Your_Authorized_Party_ID>"
              }
            }
          }
        ]
      }
      ```
  *   Create and attach a policy granting permissions to access your queue ARN. The policy must allow `sqs:ListQueues` and `sqs:SendMessage`. Verify your resource matches your exact queue ARN. For example:

      ```programlisting
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Sid": "AllowLogsToSQS",
            "Effect": "Allow",
            "Action": [
              "sqs:GetQueueAttributes",
              "sqs:ListQueues",
              "sqs:SendMessage"
            ],
            "Resource": [
              "arn:aws:sqs:<region>:<account_id>:<queue_name>"
            ]
          }
        ]
      }
      ```
* **IAM access keys**: Verify the user associated with the access key and secret key has related permissions to accept the data.

### Complete external application configuration in Cortex XSIAM

1. Go back to Cortex XSIAM and enter the instance name and an optional description.
2. Select either **IAM Role** or **IAM Access Keys**.
   * For IAM role, paste the role ARN (Amazon Resource Name) from the role you created.
   * For IAM access keys, enter the access key and secret key.
3. Click **Test** to verify Cortex XSIAM can write a test object, then click **Connect**.

### Configure notification forwarding

Follow the instructions for [Configure notification forwarding](../configure-notification-forwarding).
