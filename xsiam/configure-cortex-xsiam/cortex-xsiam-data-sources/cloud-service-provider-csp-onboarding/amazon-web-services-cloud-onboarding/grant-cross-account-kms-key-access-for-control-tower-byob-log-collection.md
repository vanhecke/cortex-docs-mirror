---
description: >-
  Learn how to configure cross-account AWS KMS key permissions for Cortex
  Control Tower BYOB log collection. Step-by-step guide to updating KMS key
  policies.
---

# Grant cross-account KMS key access for Control Tower BYOB log collection

This procedure is required if you are using custom Control Tower (BYOB) log collection and you choose to encrypt your logs with a KMS key.

When a KMS key and the accessing IAM role reside in different AWS accounts, AWS requires a two-way trust handshake to authorize access:

* IAM side (Automated): The Cortex XSIAM CloudFormation template automatically attaches `kms:Decrypt` permissions for your specified key ARN to the `cortex-logs-ingestion-access-<resource-suffix>` role in the Log Archive account.
* KMS key policy side (Manual): You must update the KMS key's resource policy to explicitly trust and allow the Cortex XSIAM IAM role in the Log Archive account to perform the `kms:Decrypt` action.

{% hint style="info" %}
#### Prerequisites

Before you begin, retrieve and note the following values:

* **Logging account ID**: The 12-digit AWS account ID of your logging account where the Cortex IAM role is deployed.
* Cortex role name: The exact name of the IAM role created by the Cortex XSIAM CloudFormation template in the Log Archive account (e.g., `cortex-logs-ingestion-access-<resource>-<suffix>`). You can retrieve this from the **Outputs** tab of the deployed CloudFormation stack.
* KMS key ID or ARN: The identifier of the KMS key used to encrypt your Control Tower S3 bucket.
{% endhint %}

1. Sign in to the AWS Management Console of the Management account where the KMS key resides.
2. Navigate to **Key Management Service (KMS) > Customer managed keys**.
3. Select the KMS key used to encrypt your Control Tower S3 bucket.
4. Select the **Key policy** tab, then click **Edit**.
5. In the JSON editor, locate the closing bracket (`]`) of the `Statement` array.
6.  Append a comma (`,`) to the statement immediately preceding the closing bracket, then paste the following block:

    ```json
    {
      "Sid": "AllowCortexCrossAccountKmsDecrypt",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<LOGGING_ACCOUNT_ID>:role/<CORTEX_ROLE_NAME>"
      },
      "Action": "kms:Decrypt",
      "Resource": "*"
    }
    ```

    Where:

    * `<LOGGING_ACCOUNT_ID>` is your 12-digit Log Archive account ID.
    * `<CORTEX_ROLE_NAME>` is the full name of your Cortex IAM role.
7. Click **Save changes**.

### Verify connection

Once the key policy is updated, verify that Cortex XSIAM can successfully decrypt and ingest the logs:

1. Log in to Cortex XSIAM.
2. Navigate to **Settings > Data Sources & Integrations > Cloud Accounts**.
3. Locate your cloud instance and verify that the Audit Log status indicator is green.

Troubleshooting: If the status indicator remains red, verify that both the Log Archive account ID and the Cortex IAM role name in your KMS key policy statement match the values listed in your CloudFormation stack outputs exactly.
