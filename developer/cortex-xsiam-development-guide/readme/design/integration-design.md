---
description: Cortex XSIAM guidance for designing reliable, documented integrations.
---

# Integration design

Integrations enable communications with third-party APIs. If you are contributing an integration to Marketplace, you must follow the [design best practices](design-best-practices). To be accepted in the Cortex XSIAM Marketplace, integrations must function correctly, be properly documented, and work well with other related content.

When designing an integration, consider the following questions:

* Which product/API are you integrating with?
* Which product category does it belong to? See the list of approved [product categories](https://github.com/demisto/content/blob/master/Tests/Marketplace/approved_categories.json).
* Which version(s) of the product will you support?
* How does the authentication work?
* Will your integration fetch alerts? If so, what are the names of the entities in the source product (for example alerts, events, messages, warnings, logs) that will be mapped to alerts in Cortex XSIAM? What is the lifecycle of the entities, are they static or are they updated over time?
* What is the maximum number of new alerts this product can generate in a busy production environment?
* Are you calling APIs that can take longer than 5 to 10 seconds to respond?
* Does the product provide feeds of IOCs?
* Does the product provide any reputation on Indicators of Compromise (IOCs)?

**Additional Considerations**

* Understand and follow our code conventions to simplify implementation and the review process.
  * [Python](../../integrations-and-scripts/developing/python-code-conventions)
  * [PowerShell](../../integrations-and-scripts/developing/powershell)
* Integrations run in [Docker](../../integrations-and-scripts/developing/using-docker) containers. Cortex XSIAM provides generic images with recent Python and PowerShell versions and a small set of libraries. To use additional libraries that are not part of the default images, view our [dockerfiles](https://github.com/demisto/dockerfiles) repository in GitHub to see if an existing images meets your needs. If not, you can create your own Docker image and [contribute it](https://github.com/demisto/dockerfiles/blob/master/README.md). The Docker image to use must be specified in the integration YAML file.
* You can build feed integrations that collect batches of indicators from threat intel feeds. For more information, see [Feed Integrations](../../integrations-and-scripts/advanced-topics/feed-integrations).
* To store integration-specific data, such as tokens that have a specific duration (i.e. JWTs for authentication), you can use the [integration cache](../../integrations-and-scripts/advanced-topics/integration-cache) functionality.
