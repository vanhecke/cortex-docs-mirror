# Forward notifications to Amazon S3

Create the S3 Bucket

1. Log in to your AWS Management Console.
2. Navigate to S3 and click **Create bucket**.
3. Enter a unique bucket name and select the AWS Region. Note the region, as you will need it later.
4. Verify **Block all public access** is turned on for security.

Configure egress in Cortex Gateway

Before forwarding cases or issues to Amazon S3, you need to configure egress. Only a user with Account Admin or Instance Admin permissions can configure egress.

To configure egress, you must enter the bucket name. For example, if the full path is `s3://parent-bucket-name/child-bucket/`, enter `parent-bucket-name`.

1. In the Cortex Gateway, go to **Permission Management** → **Egress Configurations** → **Path**.
2. Select the account name and tenant.
3. In the Flow field, select **External Storage: AWS S3**.
4. Enter the exact `<bucket_name>`. For example, `my-example-bucket`. Do not include subfolders.
5. Add the configuration.

Generate the authorized party ID

1. In Cortex XSIAM, go to **Settings** → **Configurations** → **Integrations** → **External Applications** → **Add Application** and select **Amazon S3**.
2. Enter the S3 URI.
3. Click **Verify**. If egress has not been configured in the Cortex Gateway, verification will fail and a message will display that the endpoint does not match any approved routes.
4. After verification is successful, an authorized party ID is generated. Copy this ID for your AWS configuration.
5. Leave this page open to complete the application configuration after configuring the IAM role and permissions in AWS.

Configure the IAM Role and permissions in AWS

Cortex XSIAM needs permission to assume a role in your account.

1.  In AWS, go to **IAM** → **Roles** → **Create role**, select Custom trust policy, and enter the Trusted Entity JSON, replacing the sub condition with your Authorized party ID. The following is an example:

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
2.  Create and attach a policy granting permissions.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The policy must allow <code>s3:PutObject</code> and <code>s3:ListBucket</code>. Verify the resource matches your exact bucket name, formatted as <code>arn:aws:s3:::your-bucket-name/*</code>. The following is an example:</p><pre class="language-programlisting"><code class="lang-programlisting">{
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "Statement1",
          "Effect": "Allow",
          "Action": [
            "s3:PutObject",
            "s3:ListBucket"
          ],
          "Resource": [
            "arn:aws:s3:::&#x3C;your-bucket-name>/*"
          ]
        }
      ]
    }
    </code></pre></div>

Complete external application configuration in Cortex XSIAM

1. Go back to Cortex XSIAM and enter the instance name and an optional description.
2. Select **IAM Role** as the connection method and paste the Role ARN (Amazon Resource Name) from the role you created.
3. Enter the AWS region. The region you select must exactly match the bucket's region in AWS.
4.  Select the file rollup time to collect data (cases or issues) before sending. The default is one hour. This is the maximum duration the system collects data before writing to a new file in Amazon S3.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The first message is always sent immediately, and the selected rollup time applies to all subsequent data</p></div>
5. Click **Test** to verify Cortex XSIAM can write a test object, then click **Connect**.

Configure notification forwarding

Follow the instructions for [Configure notification forwarding](../configure-notification-forwarding).
