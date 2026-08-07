---
description: >-
  Define your use case, how to improve your incident workflow and decrease the
  time and resources required for investigation.
---

# Use Case Design for Cortex XSIAM

When designing your use case, consider how you want to create alerts, enrich data, and respond to alerts.

*   Alert creation

    Alerts can be fetched from external APIs or pushed to Cortex XSIAM using REST APIs or emails. Custom layouts can also be created to allow the SOC analyst to focus on the most relevant information.
*   Data enrichment

    Additional data is automatically collected from multiple sources (including directories and databases) to provide the analyst with all the necessary context to make decisions on priority and impact.
*   Alert response

    This can range from closing a false positive to complex playbooks including automated or semi-automated remediation steps across the entire IT infrastructure, such as blocking, quarantining, notifying people, collecting more data, forensics analysis, reporting, etc.

When you begin designing a content pack, we recommend you start by thinking about user stories. What would be a successful outcome for the user? How can you improve your incident workflow and decrease the time and resources required for investigation? The following points can help you design your contribution:

* Do you want to create an end-to-end use case that includes all of the phases of alert creation, data enrichment, and incident response?
* Do you want Cortex XSIAM to consume alerts from a new product?
* Do you want to provide enrichment from a data or reputation source that isn't already available in content?
* Do you want to automatically fetch IOCs from a third party platform into Cortex XSIAM?
* Do you want to map a third party product API into Cortex XSIAM, so that actions can be automated?
* Do you want to create playbooks that automate a response workflow across multiple security products?
* Are there time-consuming manual tasks in your products or security department that could be automated?

The following are examples of use cases:

* The SOC team wants to include a new source of alerts in Cortex XSIAM from a security product that is currently not supported by Marketplace. This could be already achieved through a SIEM, but a direct integration makes it easier to consume and provide a better UX to the analysts.
* The SOC team wants Cortex XSIAM to automatically provide reputation information about IOCs from a Threat Intelligence source that is currently not supported by Cortex XSIAM.
* The SOC team wants to integrate to an existing IT solution (i.e. a CMDB, Instant Messaging platform or Database) to automatically exchange data with Cortex XSIAM.
* The SOC team wants to automatically trigger actions on a third party security product that is currently not available in the Marketplace.

You can also view more [use cases](../../documentation/content-pack-metadata-file) across a variety of product categories.

If you are a third-party security vendor and want to integrate your product, we encourage you to think creatively about your product's unique capabilities that can be provided through Cortex XSIAM to provide value to joint customers. We recommend not limiting the use case to your existing APIs, during the design phase. In some cases, when creating a content contribution, technology partners decide to implement new APIs in their platforms to improve automation and better integrate with Cortex XSIAM.
