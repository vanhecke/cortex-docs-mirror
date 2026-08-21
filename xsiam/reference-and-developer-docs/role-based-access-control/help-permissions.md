---
description: >-
  Control access to create and manage in-product technical support cases  in
  Cortex XSIAM.
---

# Help permissions

**Support**

Allows users to create, view, and manage technical support cases by going to **Help** → **In-App Help Center**.

For more information, see [In-product support case creation](../../learn-about-cortex-xsiam/in-product-support-case-creation).

{% hint style="warning" %}
### Caution

The tenant must have an active support contract, and the user must have CSP portal access.
{% endhint %}

| Permission | Description                                                                                                                                                                                                                                                                                                                                                       | Roles Example                                     |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| None       | The user can't submit support cases.                                                                                                                                                                                                                                                                                                                              |                                                   |
| View/Edit  | <p>Enables users to submit support tickets directly from within Cortex XSIAM. This includes:</p><ul><li>Creating new support cases with Palo Alto Networks support.</li><li>Attaching files and recordings to support tickets.</li><li>Generating Technical Support Files (TSF) from endpoints.</li><li>Recording browser sessions for troubleshooting.</li></ul> | All roles should be able to submit support cases. |

**Required and recommended permissions**

Consider adding the following permissions:

| Permission                        | Permission Level | Reason                                                                                                                                                                                                                                                                         |
| --------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Retrieve Endpoint Data            | Checked          | Enables TSF (Technical Support File) generation from endpoints directly within the support case wizard. Without this, users cannot attach endpoint diagnostic data to tickets, significantly reducing support effectiveness for endpoint-related issues. Strongly recommended. |
| Agent Administrations             | View/Edit        | Strongly recommended to view and select endpoints in the support case form. Without this, the endpoint selection dropdown is disabled. Users cannot pick a specific endpoint to associate with their ticket.                                                                   |
| Agents (Cortex Agentic Assistant) | View/Edit        | Enables agent-related permissions within the support case form. When present, it allows the user to include the agent context in support tickets. Recommended.                                                                                                                 |
| Cases & Issues                    | View             | Recommended to enable users to reference and attach issue/case context when submitting support cases about detection issues.                                                                                                                                                   |
