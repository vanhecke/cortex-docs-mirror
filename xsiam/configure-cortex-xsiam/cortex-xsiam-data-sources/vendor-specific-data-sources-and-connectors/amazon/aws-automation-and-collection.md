---
description: Use AWS Automation and Collection in Cortex XSIAM.
---

# AWS Automation and Collection

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../../marketplace).
{% endhint %}

Integrate with Amazon Web Services (AWS) to automate and orchestrate security operations across AWS services. This connector runs automation and remediation commands, fetches issues, collects logs and events, ingests threat intelligence indicators, and retrieves secrets across services such as EC2, IAM, GuardDuty, Security Hub, S3, Lambda, CloudTrail, CloudWatch Logs, Organizations, WAF, EKS, DynamoDB, and Secrets Manager.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [Amazon DynamoDB](https://xsoar.pan.dev/docs/reference/integrations/amazon-dynamo-db): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - AccessAnalyzer](https://xsoar.pan.dev/docs/reference/integrations/aws---access-analyzer): Amazon Web Services IAM Access Analyzer. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - ACM](https://xsoar.pan.dev/docs/reference/integrations/aws---acm): Amazon Web Services Certificate Manager Service (ACM). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - Athena - Beta](https://xsoar.pan.dev/docs/reference/integrations/aws---athena---beta): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - CloudTrail](https://xsoar.pan.dev/docs/reference/integrations/aws---cloud-trail): Amazon Web Services CloudTrail. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - CloudWatchLogs](https://xsoar.pan.dev/docs/reference/integrations/aws---cloud-watch-logs): Amazon Web Services CloudWatch Logs (logs). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - EC2](https://xsoar.pan.dev/docs/reference/integrations/aws---ec2): Amazon Web Services Elastic Compute Cloud (EC2). This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Runtime Security, or Cortex AgentiX license.
* [AWS - GuardDuty](https://xsoar.pan.dev/docs/reference/integrations/aws---guard-duty): Amazon Web Services Guard Duty Service (gd). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - GuardDuty Event Collector](https://xsoar.pan.dev/docs/reference/integrations/aws---guard-duty-event-collector): Amazon Web Services Guard Duty Service (gd) event collector integration for Cortex XSIAM. This sub-capability is available with any active Cortex XSIAM license.
* [AWS - IAM](https://xsoar.pan.dev/docs/reference/integrations/aws---iam): Amazon Web Services Identity and Access Management (IAM). This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.
* [AWS - IAM Identity Center](https://xsoar.pan.dev/docs/reference/integrations/aws---iam-identity-center): Amazon Web Services IAM Identity Center. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - Lambda](https://xsoar.pan.dev/docs/reference/integrations/aws---lambda): Amazon Web Services Serverless Compute service (lambda). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - Organizations](https://xsoar.pan.dev/docs/reference/integrations/aws---organizations): Manage Amazon Web Services accounts and their resources. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - Route53](https://xsoar.pan.dev/docs/reference/integrations/aws---route53): Amazon Web Services Managed Cloud DNS Service. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - S3](https://xsoar.pan.dev/docs/reference/integrations/aws---s3): Amazon Web Services Simple Storage Service (S3). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - Security Hub](https://xsoar.pan.dev/docs/reference/integrations/aws---security-hub): Amazon Web Services Security Hub Service. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - SNS](https://xsoar.pan.dev/docs/reference/integrations/aws---sns): Amazon Web Services Simple Notification Service (SNS). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - SQS](https://xsoar.pan.dev/docs/reference/integrations/aws---sqs): Amazon Web Services Simple Queuing Service. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS - System Manager](https://xsoar.pan.dev/docs/reference/integrations/aws---system-manager): AWS Systems Manager is the operations hub for your AWS applications and resources and a secure end-to-end management solution for hybrid cloud environments that enables safe and secure operations at scale. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS Feed](https://xsoar.pan.dev/docs/reference/integrations/aws-feed): This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS Network Firewall](https://xsoar.pan.dev/docs/reference/integrations/aws-network-firewall): AWS Network Firewall is a stateful, managed network firewall and intrusion detection and prevention service for Amazon Virtual Private Cloud (Amazon VPC). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS Sagemaker](https://xsoar.pan.dev/docs/reference/integrations/aws-sagemaker): AWS Sagemaker - Demisto Phishing Email Classifier. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS Security Hub Event Collector](https://xsoar.pan.dev/docs/reference/integrations/aws-security-hub-event-collector): An XSIAM event collector integration for AWS Security Hub. This sub-capability is available with any active Cortex XSIAM license.
* [AWS Security Lake](https://xsoar.pan.dev/docs/reference/integrations/aws-security-lake): Amazon Security Lake is a fully managed security data lake service. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS-EKS](https://xsoar.pan.dev/docs/reference/integrations/aws-eks): The AWS EKS integration allows for the management and operation of Amazon Elastic Kubernetes Service (EKS) clusters. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS-ILM](https://xsoar.pan.dev/docs/reference/integrations/aws-ilm): Integrate with AWS's services to execute CRUD and Group operations for employee lifecycle processes. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AwsSecretsManager](https://xsoar.pan.dev/docs/reference/integrations/aws-secrets-manager): AWS Secrets Manager helps you to securely encrypt, store, and retrieve credentials for your databases and other services. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS-SNS-Listener](https://xsoar.pan.dev/docs/reference/integrations/aws-sns-listener): Amazon Simple Notification Service (SNS) is a managed service that provides message delivery from publishers to subscribers. This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.
* [AWS-WAF](https://xsoar.pan.dev/docs/reference/integrations/aws-waf): Amazon Web Services Web Application Firewall (WAF). This sub-capability is available with any active Cortex XSIAM or Cortex AgentiX license.

To configure this connector, follow the steps outlined in the configuration wizard.
