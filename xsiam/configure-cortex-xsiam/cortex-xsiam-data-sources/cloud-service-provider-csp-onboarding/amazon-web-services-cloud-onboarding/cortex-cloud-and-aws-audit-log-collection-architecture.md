---
description: Understand AWS audit log collection architecture for Cortex XSIAM.
---

# Cortex XSIAM and AWS audit log collection architecture

Cortex XSIAM collects AWS CloudTrail logs for security analysis using an event-driven, cross-cloud architecture. When audit log collection is enabled, a CloudFormation stack deploys AWS resources that capture CloudTrail events and make them available for Cortex XSIAM to ingest into your dedicated single-tenant log storage (a Google Cloud Storage bucket in Cortex XSIAM's GCP backend).

Cortex XSIAM supports collection across three organizational scopes: single account, organizational unit (OU), and full organization. It operates in both Commercial and GovCloud AWS partitions. For the complete list of resources created, see [Log collection resources](../aws-resource-inventory#log-collection-resources).

{% hint style="warning" %}
If you configure custom (BYOB) audit log collection using an existing S3 bucket, ensure that you deploy the stack in the same region as your S3 bucket. The SNS topic and SQS queue created by the stack must reside in the same region as the bucket for S3 event notifications to function.
{% endhint %}

### **Event-driven ingestion flow**

The following stages describe the event-driven ingestion flow for CloudTrail logs:

1. CloudTrail writes gzip-compressed JSON log files to the designated S3 bucket. The trail is multi-region, so it captures activity from every AWS region, and also includes global service events from non-regional services such as IAM, STS, and CloudFront.
2. CloudTrail publishes a log file delivery notification directly to the SNS topic. The notification contains the S3 bucket name and the list of new S3 object keys.
3. The SNS topic fans the notification out to its subscribers.
4. The SQS queue receives the notification and stores the S3 path pointer to the new log file.
5. Cortex XSIAM polls the SQS queue for new log notifications using **sqs:ReceiveMessage**, authenticating via the CloudTrailReadRole assumed through Google OIDC federation.
6. Cortex extracts the S3 path from the SQS message and downloads the specific log files using **s3:GetObject**.
7. Cortex decrypts the logs using the KMS key. The gzip-compressed content is then decompressed.
8. Cortex forwards the processed logs to your dedicated Cortex single tenant (GCS bucket).
9. Cortex deletes the processed SQS message using **sqs:DeleteMessage**.
10. The Cortex XSIAM instance processes the logs for security analysis.

### **Data security for audit logs**

In automated log collection mode, CloudTrail logs are retained in the S3 bucket for seven days (per the bucket's lifecycle expiration rule), and then automatically deleted. In custom (BYOB) and custom Control Tower log collection mode, you manage the S3 bucket lifecycle and retention. In all modes, forwarded log files are stored in your dedicated single-tenant Cortex XSIAM log storage bucket. CloudTrail log files at rest in the customer's S3 bucket are encrypted using the CloudTrail logs CMK (a customer-managed KMS key in your AWS account).

### **Key Management Service (KMS) considerations**

CloudTrail log files are encrypted at rest in the customer's S3 bucket. How the KMS key is provisioned depends on the deployment mode:

| Aspect                     | Automated log collection                                                                                                                                                                                                                                                              | Custom (BYOB) log collection                                                                                                                                         | Custom Control Tower log collection                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| KMS key creation           | Cortex XSIAM creates a new Customer Managed Key (CMK) via CloudFormation.                                                                                                                                                                                                             | No KMS key is created. The customer supplies the optional `CloudTrailKmsArn` parameter at deployment time.                                                           | No KMS key is created. The customer supplies the optional `CloudTrailKmsArn` parameter at deployment time.                                                                                                                                                                                                                                                                                                                                                           |
| Key policy                 | The Cortex XSIAM-created CMK uses the standard account-root key policy, which delegates access management to IAM. The `CloudTrailReadRole` role's inline IAM policy (provisioned by the same template) grants `kms:Decrypt` on the CMK, so no customer key-policy edits are required. | The customer's KMS key policy must explicitly allow the `CloudTrailReadRole` role to perform `kms:Decrypt`.                                                          | The KMS key used by Control Tower resides in the management account, while the Cortex IAM role is deployed into the logging account. Because the key and the role are in different accounts, the KMS key policy in the management account must explicitly allow the `CloudTrailReadRole` role (in the logging account) to perform `kms:Decrypt`. See [Grant cross-account KMS key access](grant-cross-account-kms-key-access-for-control-tower-byob-log-collection). |
| Role permission            | The audit log reader role inline policy includes `kms:Decrypt` on the Cortex XSIAM-created CMK.                                                                                                                                                                                       | If `CloudTrailKmsArn` is provided, the role inline policy includes `kms:Decrypt` scoped to that ARN. If left empty, the `kms:Decrypt` statement is omitted entirely. | If `CloudTrailKmsArn` is provided, the role inline policy includes `kms:Decrypt` scoped to that ARN. If left empty, the `kms:Decrypt` statement is omitted entirely.                                                                                                                                                                                                                                                                                                 |
| Unencrypted/SSE-S3 buckets | Not applicable (Cortex XSIAM always creates an encrypted bucket).                                                                                                                                                                                                                     | If the bucket uses SSE-S3 or no encryption, leave the `CloudTrailKmsArn` parameter empty.                                                                            | If the bucket uses SSE-S3 or no encryption, leave the `CloudTrailKmsArn` parameter empty.                                                                                                                                                                                                                                                                                                                                                                            |

You must use a customer-managed KMS key (CMK), not an AWS-managed or AWS-owned key. CloudTrail requires a symmetric CMK for trail encryption, and the audit log reader role must be granted kms:Decrypt through the key policy, which is only configurable on customer-managed keys.

{% hint style="info" %}
#### Note: Custom Control Tower (BYOB) log collection with KMS encryption

If you provide a `CloudTrailKmsArn` and the KMS key resides in a different account than the Log Archive account, a manual step is required. The Cortex CloudFormation template automatically grants `kms:Decrypt` to the `cortex-logs-ingestion-access-<resource-suffix>` role on the IAM side, but AWS also requires the KMS key resource policy to explicitly allow access from the Log Archive account. You must manually add this statement to the KMS key policy to complete the cross-account handshake. For the full procedure, see [grant-cross-account-kms-key-access-for-control-tower-byob-log-collection](grant-cross-account-kms-key-access-for-control-tower-byob-log-collection "mention").
{% endhint %}

### **The bucket cleanup function lifecycle**

The bucket cleanup function automates the cleanup of AWS resources to ensure a successful stack deletion. This function empties the Cortex XSIAM CloudTrail log bucket during the CloudFormation stack deletion process. Because AWS prevents you from deleting S3 buckets that are not empty, this function ensures automated cleanup without manual intervention.

The bucket cleanup function operates only during the deletion of the CloudFormation stack. For security, the function has permissions to delete objects only from the specific CloudTrail bucket and cannot access or delete objects from other S3 buckets.

{% hint style="info" %}
This resource only exists in automated log collection mode, because Cortex XSIAM only creates and owns the S3 bucket in that mode. In BYOB mode, the customer owns and manages their own bucket and its lifecycle.
{% endhint %}
