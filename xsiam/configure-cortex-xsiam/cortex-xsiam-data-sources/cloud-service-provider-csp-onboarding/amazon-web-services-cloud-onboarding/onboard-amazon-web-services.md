---
description: >-
  Follow the AWS onboarding wizard, and Cortex XSIAM creates a custom
  authentication template to be executed in AWS.
---

# Onboard Amazon Web Services

Use the cloud onboarding wizard to integrate an Amazon Web Services (AWS) environment with Cortex XSIAM. The onboarding wizard requires minimal configuration to set up the integration. To complete the minimum configuration, define the scope of the AWS accounts and specify the scan mode. Alternatively, configure the advanced settings for full control of the onboarding process.

Cortex XSIAM generates an authentication template based on the configuration settings. The template establishes trust with AWS and creates the required resources. For account scope, you can choose to deploy the template using CloudFormation or Terraform. For organization and organizational unit scope, CloudFormation is used. Execute the template to complete the onboarding process. Executing the template notifies Cortex XSIAM of the execution details. Cortex XSIAM then creates a new cloud instance.
