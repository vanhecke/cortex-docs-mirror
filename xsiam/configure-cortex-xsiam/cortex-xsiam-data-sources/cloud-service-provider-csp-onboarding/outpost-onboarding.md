---
description: >-
  Learn about outposts, which are a dedicated set of infrastructure resources
  that extends the reach of Cortex XSIAM into your environment.
---

# Outpost onboarding

{% hint style="info" %}
**License type**: This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM product that has the Cloud Runtime Security add-on.
{% endhint %}

An outpost is a dedicated set of infrastructure resources that extends the reach of Cortex XSIAM into your environment. It serves as a secure, localized point for scanning assets across cloud providers and on-premises workloads.

By establishing a trusted relationship between Palo Alto Networks and your environment, the outpost allows for deep security analysis, such as identifying vulnerabilities or classifying sensitive data, while ensuring that your live workloads remain unaffected. This architecture helps you maintain strict data residency and compliance by performing scans locally within a demarcated area of your network.

{% hint style="warning" %}
**Important**: Outpost scan is an alternative to the recommended standard cloud scan. Cloud scan is recommended because it is fully managed by Palo Alto Networks and incurs minimal compute costs for your organization. Outpost scan is an advanced deployment model reserved for specific data residency or architectural requirements.
{% endhint %}

Basic, standard outposts are the recommended deployment path for most organizations. Cortex XSIAM generates a Terraform template tailored to the values you enter in the outpost creation wizard, and you run that template in your CSP account to provision every resource the outpost needs, such as VPC or VNet, subnets, storage, secret vault, IAM roles or service accounts, scanner managed identities, and the trust relationship back to Cortex XSIAM.

This approach gives you the fastest, most consistent path to coverage while keeping the number of manual steps low. Cortex owns the resource definitions, naming conventions, and network topology, and you own the CSP account they run in.

### What outposts include

A standard outpost deployment covers the full outpost lifecycle end to end:

* **Provisioning.** Cortex-generated Terraform creates all outpost infrastructure in your CSP account, including networking, storage, secret vault, IAM roles, scanner managed identities, and optionally, for Azure, the Entra ID app registration and its federated identity credentials.
* **Trust establishment.** The template configures the trust relationship between your CSP account and Cortex XSIAM automatically, using federated identity credentials rather than long-lived secrets.
* **Registration.** Once the Terraform apply completes for both the outpost and the CSP onboarding overall, your cloud environment sends a registration callback to Cortex XSIAM, and the outpost transitions from **Pending** to **Connected**.
* **Ongoing scanning.** After the outpost reaches **Connected**, Cortex schedules scans against the resources you onboard.

#### **What's Next?**

* [Review outpost fundamentals](outpost-onboarding/outpost-fundamentals-and-planning)
* [Plan your outpost](outpost-fundamentals-and-planning#outpost-planning)
* [Create your outpost](outpost-onboarding/outpost-creation-workflow)

<br>
