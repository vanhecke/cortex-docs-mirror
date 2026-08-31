---
description: Configure application criteria for asset management in Cortex XSIAM.
---

# Application criteria

You can define and group assets into applications using two primary methods:

* **New Application:** **Manually build an application** by selecting starting assets from either the **code side** (VCS repositories) or the **run side** (cloud providers, Kubernetes clusters, or VPCs). Cortex XSIAM automatically identifies and adds related assets based on their connections.
* **New Criteria:** Automatically create and maintain applications in bulk by defining dynamic rules. You can base these criteria on **Cloud tags** (such as AWS tags grouping assets within a single provider), or **VCS entities** (automatically generating applications based on your code hierarchy, such as GitHub organizations or repositories).

Go to **Inventory** → **Assets** → **Configurations** → **Application Criteria** to add a new application or new criteria.

For more information, see: [Defining Business Applications](https://app.gitbook.com/s/8Z0RLJ1BFF5TQL8VtUeK/application-security-posture-management-aspm/applications/defining-business-applications).

For information on defining applications, see [Defining Business Applications](../asset-classes/application-assets).
