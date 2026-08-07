---
description: Before you begin onboarding GCP, you must review the following prerequisites.
---

# Prerequisites for onboarding GCP

## Permissions

Before you begin to onboard GCP to Cortex XSIAM, ensure that you have the necessary permissions:

* In Cortex XSIAM, you must have a Cortex XSIAM role with Data Sources - View & Edit permissions (to add/configure cloud accounts in Cortex XSIAM). This role is included in the following built-in roles: Instance Administrator, Security Admin, and IT Admin.
* In GCP, you must have access to Google Cloud console and an admin user with the required [GCP permissions](#required-admin-gcp-permissions-for-cortex-xsiam-onboarding).

## Required APIs

Ensure you have enabled the following APIs in the GCP project you are onboarding:

* [Cloud Resource Manager API](https://console.cloud.google.com/apis/api/cloudresourcemanager.googleapis.com)
* [Identity and Access Management (IAM) API](https://console.cloud.google.com/apis/api/iam.googleapis.com)
* [Cloud Pub/Sub API](https://console.cloud.google.com/apis/api/pubsub.googleapis.com) (if audit logs are enabled)

If you plan on enabling Automation as an additional security capability, enable the following APIs:

* [Kubernetes Engine API](https://console.cloud.google.com/apis/api/container.googleapis.com)
* [Compute Engine API](https://console.cloud.google.com/apis/api/compute.googleapis.com)
* [Service Usage API](https://console.cloud.google.com/apis/api/serviceusage.googleapis.com)
* [Cloud Storage API](https://console.cloud.google.com/apis/api/storage-component.googleapis.com)

### Required admin GCP permissions for Cortex XSIAM onboarding

Use the following template to create a dedicated role with the permissions required for onboarding GCP to Cortex XSIAM:

```json
{
  "title": "CortexCloudOnboarding",
  "description": "Custom role with permissions required for onboarding Cortex XSIAM",
  "stage": "GA",
  "includedPermissions": [
    "iam.roles.create",
    "iam.roles.delete",
    "iam.roles.get",
    "iam.roles.list",
    "iam.roles.update",
    "iam.serviceAccounts.create",
    "iam.serviceAccounts.delete",
    "iam.serviceAccounts.get",
    "iam.serviceAccounts.getIamPolicy",
    "iam.serviceAccounts.list",
    "iam.serviceAccounts.setIamPolicy",
    "iam.serviceAccounts.update",
    "logging.sinks.create",
    "logging.sinks.delete",
    "logging.sinks.get",
    "logging.sinks.update",
    "pubsub.subscriptions.create",
    "pubsub.subscriptions.delete",
    "pubsub.subscriptions.getIamPolicy",
    "pubsub.subscriptions.setIamPolicy",
    "pubsub.subscriptions.update",
    "pubsub.topics.create",
    "pubsub.topics.delete",
    "pubsub.topics.getIamPolicy",
    "pubsub.topics.setIamPolicy",
    "pubsub.topics.update",
    "resourcemanager.folders.get",
    "resourcemanager.folders.getIamPolicy",
    "resourcemanager.folders.list",
    "resourcemanager.folders.setIamPolicy",
    "resourcemanager.organizations.get",
    "resourcemanager.organizations.getIamPolicy",
    "resourcemanager.organizations.setIamPolicy",
    "resourcemanager.projects.get",
    "resourcemanager.projects.getIamPolicy",
    "resourcemanager.projects.list",
    "resourcemanager.projects.setIamPolicy"
  ]
}
```
