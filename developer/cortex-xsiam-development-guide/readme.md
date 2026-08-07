---
description: "Get started developing content for\_Cortex XSIAM."
---

# Getting Started

This guide helps you create Cortex XSIAM content. You can create content for your own use, or contribute content to Marketplace that either you support or that is community supported.

Playbooks, alert fields/layouts/rules, indicator fields/types/layouts, classifiers, mappers, widgets, and dashboards should be developed within the Cortex XSIAM UI.

For integrations and scripts, when creating content to use within your instance of Cortex XSIAM or for contribution as a community supported content pack, the UI may be sufficient. For more complex development needs, or if you plan on contributing content as a partner supported content pack or a modification to partner supported content, we recommend using Visual Studio Code, with the [Visual Studio Code extension](readme/content-development-environments/visual-studio-code-extension). If you work locally, we recommend installing [Demisto SDK](readme/content-development-environments/demisto-sdk) to upload, download, and run code on Cortex XSIAM directly from your operating system shell. To develop content for contribution as a partner-supported content pack, or to submit modifications to partner-supported content packs, you must set up a [full development environment](readme/content-development-environments).

If you have questions or need support, contact us on the `#demisto-developers` channel on our [DFIR Slack community](https://start.paloaltonetworks.com/join-our-slack-community).

### Prerequisites and resources

Cortex XSIAM is a powerful platform with a rich set of features and customizations. We recommend following these steps before creating custom content:

1. Read and understand Cortex XSIAM [Concepts](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/).
2. Read the [FAQs](readme/frequently-asked-questions).
3. Review relevant sections of the Cortex XSIAM product [documentation](https://app.gitbook.com/o/r4DIGbR5VLvkZy3gAYsu/s/XO7Budkunf9O78igMwUM/).
4.  Understand your use case.

    What are you trying to achieve? What is the user story? What is the expected workflow? Are you creating a content pack or creating content for internal use?
5.  Development scope

    What content items do you need to develop? Content can include integrations, scripts, playbooks, dashboards, fields, layouts, classifiers, mappers, lists, and data modeling and parsing rules. In some cases, you may just need a playbook to achieve your goals. In other cases, you may need multiple content items.
6. Verify you have an [active tenant](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam).
7. If you plan to publish your content to Marketplace for other customers to use, read about the [contribution process](contributing-content) and the different tiers and support levels (for example, partner vs community support). Learn about best practices and requirements for content pack contributions.
8. Register to the [Learning Center](https://beacon.paloaltonetworks.com/student/catalog) and go through the Product Training.
9. Access the Palo Alto Networks [DFIR Slack community](https://start.paloaltonetworks.com/join-our-slack-community) and join the **`#demisto-developers`** channel.
10. If you are integrating with an external API, verify you have API or SDK access to the product or solution you want to integrate with.
11. (Optional) Install the [Demisto SDK](readme/content-development-environments/demisto-sdk).

    The Demisto SDK is a command line tool that can be used to upload, download, validate and run code on Cortex XSIAM directly from your command line. The Demisto SDK offers a Python library and CLI designed to aid the development process, to validate entities and to assist in the interaction between your development setup and Cortex XSIAM. You can use the Demisto SDK with the built-in IDE or with a full development environment.
12. (Optional) Install the Video Studio Code extension to develop integrations and scripts.

### Development, documentation, and contributions

* Development
  *   Integrations and scripts

      Review the structure for integrations and code conventions, as well as features such as data centralization, intelligent stitching, analytics-based detection, alert and incident management, script, generic commands, and reputation score. Write and test your code.
  *   Playbooks - learn about playbook design, conventions, and the use of generic playbooks.

      For more information on playbook design and development, see [Playbooks](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/).
  * Lists - learn how to download a list from Cortex XSIAM and include it in your content pack.
  * Alerts - learn how to create alert fields, layouts, rules, classifiers, and mappers.
  *   Data modeling, parsing, and correlation - learn how to create parsing, data modeling, and correlation rules.

      Enable mapping of events and logs into a single, unified data model. This data model provides a consolidated schema, and a simpler way to interact with your data, regardless of its source or dataset. To familiarize yourself with the data model schema, see [Cortex XSIAM Data Model Schema](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/).
  * **Indicators** - learn how to create indicator fields and layouts. Learn how domains and URLs are extracted, how to create and use relationships, and more.
* Documentation - learn about documentation best practices, as well as documentation requirements for Marketplace contributions.
* Contributions - learn the requirements for contributing content to Marketplace.
