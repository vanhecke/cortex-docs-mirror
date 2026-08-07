---
description: >-
  Follow the OCI onboarding wizard, and Cortex creates a custom authentication
  template to be executed in OCI.
---

# Onboard Oracle Cloud Infrastructure

Use the cloud onboarding wizard to integrate an Oracle Cloud Infrastructure (OCI) environment with Cortex XSIAM. The onboarding wizard requires minimal configuration to set up the integration. OCI onboarding operates at the tenancy (organization) scope and uses Cortex XSIAM-managed scanning. Optionally, configure the advanced settings to enable additional security capabilities such as agentless disk scanning and registry scanning, or to refine the compartment scope.

Cortex XSIAM generates a Terraform authentication template based on the configuration settings. The authentication template creates an IAM policy, an IAM group, and supporting identity resources in your OCI tenancy that grant Cortex XSIAM the required permissions. Execute the authentication template in OCI to complete the onboarding process. Executing the authentication template notifies Cortex XSIAM of the execution details. Cortex XSIAM then creates a new cloud instance.
