---
description: >-
  How to prepare for a demo and how the demo is conducted as the last stage of
  the contribution before it is merged into the content internal repo.
---

# Contribution demo preparation

A demo is the last stage required before the contribution is merged into the content internal repo. To be as prepared as possible and to avoid post-demo change requests, review all of the steps below.

{% hint style="info" %}
### Note

A contribution demo is not required for community-supported content packs.
{% endhint %}

#### General notes

* The purpose of the demo is to verify the contribution meets Cortex XSIAM standards and to check that features work as expected, while providing a satisfactory user experience.
* The contributor, the PR reviewer, and in some cases a security reviewer, participate in the the demo.
* The demo can take up to one hour.

#### Before the demo

* Verify the change requests from your code review are fully addressed and fixed.
* Prepare a Cortex XSIAM tenant that has all recent changes and has the most updated version of your content pack. The demo is performed in this environment.

#### Demo agenda and workflow

The following may vary based on the size and scope of the contribution.

| Section                                                                                                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Product Overview                                                                                        | Short general explanation about the product.                                                                                                                                                                                                                                                                                                                                                                                        |
| Use Cases Overview                                                                                      | The specific use cases for the customer.                                                                                                                                                                                                                                                                                                                                                                                            |
| Integration Commands Overview                                                                           | Review which commands are implemented.                                                                                                                                                                                                                                                                                                                                                                                              |
| Demo Integration Instance Configuration                                                                 | <ul><li>Verify it's clear how to retrieve required credentials.</li><li>Verify correct error handling - what happens when credentials are incorrect.</li></ul>                                                                                                                                                                                                                                                                      |
| Demo Integration Commands                                                                               | <p>Verify that commands, arguments, and outputs (including descriptions) are according to standard:</p><ul><li><a href="../integrations-and-scripts/developing/python-code-conventions">Python code conventions</a></li><li><a href="../integrations-and-scripts/developing/context-and-outputs">Context and outputs</a></li><li><a href="../integrations-and-scripts/developing/context-standards">Context standards</a></li></ul> |
| Demo Fetch Incidents (if applicable)                                                                    | Verify that incidents are fetched and displayed correctly.                                                                                                                                                                                                                                                                                                                                                                          |
| Demo Playbooks (if applicable)                                                                          | Verify that playbooks run as expected.                                                                                                                                                                                                                                                                                                                                                                                              |
| Review Layouts, Alert and Indicator Types, Alert and Indicator Fields, and Classifiers (if applicable). | <ul><li>Verify layout is bound to incident/indicator type.</li><li></li><li>Verify alert/indicator fields are bound to alert/indicator types.</li><li>Verify classifier is bound to incident type.</li><li>Verify playbook is bound to an incident type.</li></ul>                                                                                                                                                                  |

#### After the demo

* If changes were requested during the demo by the reviewers, make and commit these changes.
* After all requested changes are made, the PR is merged.
