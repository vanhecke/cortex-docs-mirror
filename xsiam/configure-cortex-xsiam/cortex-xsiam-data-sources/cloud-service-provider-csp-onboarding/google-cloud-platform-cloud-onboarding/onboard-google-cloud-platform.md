---
description: >-
  Follow the GCP onboarding wizard, and Cortex creates a custom authentication
  template to be executed in GCP.
---

# Onboard Google Cloud Platform

Use the cloud onboarding wizard to integrate a Google Cloud Platform (GCP) environment with Cortex XSIAM. The onboarding wizard requires minimal configuration to set up the integration. To complete the minimum configuration, define the scope of the GCP environment you are onboarding and specify the scan mode. Alternatively, configure the advanced settings for full control of the onboarding process.

Cortex XSIAM generates a Terraform authentication template based on the configuration settings. The authentication template establishes trust with GCP. The authentication template also grants required permissions to Cortex XSIAM. Execute the authentication template in GCP to complete the onboarding process. Executing the authentication template notifies Cortex XSIAM of the execution details. Cortex XSIAM then creates a new cloud instance.
