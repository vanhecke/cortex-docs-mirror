---
description: >-
  Review platforms and services supported by Cortex Cloud AI Security in Cortex
  XSIAM.
---

# Supported services in Cortex Cloud AI Security

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

The following lists the various services that are compatible with Cortex Cloud AI Security, detailing the specific platforms and services where Cortex Cloud AI Security can be effectively used to ensure security and compliance:

* **AWS:** Amazon Bedrock, Amazon SageMaker, Amazon S3 Vectors
* **Azure:** Azure AI Foundry, Azure OpenAI, Azure AI Search

{% hint style="info" %}
**Note**

Using outpost scan mode is mandatory for full AI asset discovery in Azure. In addition, DSPM must be enabled. Note that you can enable DSPM while disabling it for all non-AI services. For more information, see [How to configure the scanning settings for supported services](../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting/manage-instances/how-to-configure-the-scanning-settings-for-supported-services) and [Cloud service provider onboarding](../../configure-cortex-xsiam/cortex-xsiam-data-sources/cloud-service-provider-csp-onboarding).
{% endhint %}

* **GCP:** Vertex AI
* Self-managed AI models
* [SaaS AI Agents](../cortex-cloud-saas-security/saas-ai-agent-security)
