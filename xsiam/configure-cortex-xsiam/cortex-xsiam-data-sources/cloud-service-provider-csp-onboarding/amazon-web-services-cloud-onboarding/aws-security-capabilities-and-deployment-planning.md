---
description: Plan AWS security capabilities for Cortex XSIAM cloud onboarding.
---

# AWS security capabilities and deployment planning

Plan your deployment by selecting the appropriate security capabilities. The onboarding process deploys all selected capabilities using a single CloudFormation template that adds specific functionality to your Cortex XSIAM integration.

## Core capability (Discovery)

Discovery is a mandatory capability that is deployed automatically when you onboard an AWS account to Cortex XSIAM. Use this capability to discover and monitor AWS resources. When you onboard using a CloudFormation template, the template provisions the CortexPlatformRole AWS role along with a short-lived helper function that registers the deployment with Cortex XSIAM..

## Logging capabilities

The Audit Logs capability collects AWS CloudTrail logs for security analysis and event-driven Asset Inventory. Across all collection modes, Cortex XSIAM provisions the `CloudTrailReadRole` IAM role to grant Cortex XSIAM read access to the target Amazon S3 bucket. Three collection modes are available depending on your AWS scope:

* Custom (BYOB) audit log collection: Designed for single-account setups or standard organizations where all resources reside in a single AWS account. Use your existing S3 bucket and CloudTrail trail. Cortex XSIAM provisions the notification pipeline (SQS queue and SNS topic) and connects to your bucket to ingest logs.
* Custom Control Tower (BYOB) audit log collection: Designed for AWS organizations governed by AWS Control Tower. Because Control Tower centralizes log storage by placing the S3 bucket in a dedicated logging account and the SNS topic in a dedicated Audit account, this deployment uses a multi-account architecture:
  * IAM role deployment: Provisioned in the log archive account.
  * SQS queue deployment: Provisioned in the account holding the SNS topic to enable local event subscription and message queuing.
* Cortex automated log collection: Cortex XSIAM provisions and manages all required AWS resources (S3 bucket, CloudTrail trail, encryption, and notifications) on your behalf.

In all modes, the supporting infrastructure is deployed in a single AWS region - the region where you launch onboarding. The CloudTrail trail itself is multi-region and captures events from all AWS regions. For Custom (BYOB) mode, regional coverage matches your existing trail's configuration. For full details on deployment modes, ingestion flow, and data security, see Audit Log Collection Architecture.

| Collection mode             | Resources created                                                                                                                                                | Purpose                                                                                                                                                                                                                                                  |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Custom (BYOB)               | SQS Queue, SNS Subscription, SQS Queue Policy                                                                                                                    | <p>Connect to a customer-managed S3 bucket and CloudTrail trail.</p><p>Event notifications flow through customer-owned SQS/SNS resources.</p>                                                                                                            |
| Custom Control Tower (BYOB) | SQS Queue, SNS Subscription, SQS Queue Policy, IAM Role (`cortex-logs-ingestion-access-<resource>-<suffix>`, deployed into the Log Archive account via StackSet) | Connect to the centralized S3 bucket managed by AWS Control Tower in the logging account. The IAM role is deployed cross-account into the logging account; the SQS queue is created in the management account where the Control Tower SNS topic resides. |
| Automated                   | S3 Bucket, S3 Bucket Policy, KMS Key, CloudTrail Trail, SNS Topic, SNS Topic Policy, SNS Subscription, SQS Queue, SQS Queue Policy, Lambda Function              | Cortex XSIAM provisions the S3 bucket, CloudTrail trail, and encryption key, then collects CloudTrail logs automatically.                                                                                                                                |

## Scanning capabilities

The following table details the scanning capabilities available during cloud onboarding. The table specifies the IAM roles and resources created and the purpose of each capability. Use this reference to understand the infrastructure footprint and coverage of each scanning capability deployed by Cortex XSIAM. All scanning capabilities operate across all AWS regions in the onboarded account.

| Capability                           | Purpose                                                  | Resources created                                                                                                                                                                                                                        |
| ------------------------------------ | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agentless Disk Scanning (ADS)        | Agentless disk scanning for vulnerabilities.             | Custom managed policy **Cortex-ADS-Policy** added to **CortexPlatformRole**                                                                                                                                                              |
| Outpost Scanner                      | Enables data security, registry and serverless scanning. | **CortexPlatformScannerRole** IAM Role                                                                                                                                                                                                   |
| Data Security Scanning (DSPM)        | Data classification and sensitive data discovery.        | Managed policy **Cortex-DSPM-Policy** attached to **CortexPlatformRole**; inline **Cortex-DSPM-Scanner-Policy** embedded in **CortexPlatformScannerRole**. Adds export.rds.amazonaws.com as a trusted service on **CortexPlatformRole**. |
| Registry Scanning                    | Container image vulnerability scanning.                  | **ECRAccessPolicy** Inline policy added to CortexPlatformScannerRole                                                                                                                                                                     |
| Serverless Scanning                  | Lambda function vulnerability scanning.                  | LAMBDAAccessPolicy Inline policy added to **CortexPlatformScannerRole**                                                                                                                                                                  |
| Kubernetes Security Posture Scanning | Kubernetes posture and configuration scanning on EKS.    | Managed policy (**CortexK8sSecurityPolicy**) added to **CortexPlatformRole**                                                                                                                                                             |

## Automation capabilities

The Automation module extends AWS cloud instances with automated remediation and active response capabilities. When enabled, it provisions a managed IAM policy (**Cortex-Automation-Policy**) and attaches it to the existing **CortexPlatformRole**. This policy grants Cortex XSIAM the permissions required to execute automated actions across AWS services such as EC2, S3, IAM, RDS, Lambda, and others. The capability applies globally across all scopes (Account, Organization, and Organizational Unit) and does not require region-specific configuration.

All actions are granted on **\`Resource: "\*"\`**, so each permission applies to every resource of the affected service in every AWS region of the onboarded account. Review the full action list with your security team and enable the Automation capability only in accounts where Cortex XSIAM is authorized to perform automated remediation. For accounts intended only for monitoring, leave this capability disabled.

\
\
<br>
