---
description: >-
  Connect cloud provider accounts to scan serverless functions for security
  vulnerabilities, malware, and exposed secrets in Cortex XSIAM.
---

# Onboard cloud providers for serverless functions

Integrate Cortex XSIAM with your cloud provider accounts to enable security vulnerability, malware and exposed secret scans of your serverless functions. This enables you to efficiently analyze, prioritize, and resolve security findings specific to your serverless deployments.

{% hint style="info" %}
When scanning serverless functions with layers, those layers need to be from the same cloud account.
{% endhint %}

Supported cloud providers include:

* Amazon Web Services (AWS): Refer to [Onboard Amazon Web Services](../../configure-cortex-xsiam/cortex-xsiam-data-sources/cloud-service-provider-csp-onboarding/amazon-web-services-cloud-onboarding/onboard-amazon-web-services) for more information about integrating Cortex XSIAM with AWS Lambda functions.
*   Google Cloud Platform (GCP): Refer to [Onboard Google Cloud Platform](../../configure-cortex-xsiam/cortex-xsiam-data-sources/cloud-service-provider-csp-onboarding/google-cloud-platform-cloud-onboarding/onboard-google-cloud-platform) for more information about integrating Cortex XSIAM with GCP functions.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Cortex supports Google Cloud Functions: 1st gen and 2nd gen Cloud Functions API.</p></div>
* Microsoft Azure: Refer to [Microsoft Azure cloud onboarding](../../configure-cortex-xsiam/cortex-xsiam-data-sources/cloud-service-provider-csp-onboarding/microsoft-azure-cloud-onboarding) for more information about integrating Cortex XSIAM with Azure functions.

{% hint style="info" %}
Only functions containing zip files are supported.
{% endhint %}
