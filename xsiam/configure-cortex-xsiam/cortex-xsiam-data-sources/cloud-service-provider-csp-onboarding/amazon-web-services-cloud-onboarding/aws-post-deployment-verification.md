---
description: >-
  After you have completed the AWS onboarding wizard and you have deployed the
  authentication template in AWS (using CloudFormation or Terraform), verify
  that the deployment succeeded.
---

# AWS post-deployment verification

After you have deployed the authentication template in Amazon Web Services (AWS), verify that it was successfully deployed. In Cortex XSIAM, select **Data Sources & Integrations → Cloud Accounts**. Verify the following:

* The original cloud instance remains in "Pending" state. For more details on pending instances, see Understand pending instances.
* A new cloud instance appears in the cloud accounts list (separate from the pending instance).
* The new cloud instance shows status "Connected".
* The discovery scan starts automatically for every discovered account.
* Assets appear in the **Asset Inventory** as discovery progresses.

## Troubleshooting AWS onboarding

If no new cloud instance appears:

* Check the CloudFormation stack status in the AWS console. The status should be **CREATE\_COMPLETE**.
* Check the Lambda execution logs in AWS CloudWatch for errors. If the Lambda notification to Cortex XSIAM is not executed, Cortex XSIAM does not create a new cloud instance in Connected stated.
* You can [Manually connect an instance](../manually-connect-a-cloud-instance) to create the instance from the pending cloud instance.
