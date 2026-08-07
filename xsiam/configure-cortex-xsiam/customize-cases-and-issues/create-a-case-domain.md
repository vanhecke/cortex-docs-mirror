---
description: >-
  Create custom case domains to organize workflows, statuses, resolution
  reasons, and access.
---

# Create a case domain

{% hint style="warning" %}
Before you add a custom domain, please review the built-in options. For more information, see [Case and issue domains](../../detect-investigate-and-respond-to-threats/investigation-and-response/overview-of-cases/case-and-issue-domains).

We recommend using the built-in domains where possible. Custom domains might not be supported by all content. In addition, custom domains affect Cortex XSIAM’s ability to learn, correctly identify, and score future cases.

Smart grouping and SmartScore are not supported for custom domains.
{% endhint %}

Custom domains help you to differentiate between your work efforts. You can create tailored workflows for each domain, so that you can effectively manage and prioritize your workload.

### **Manage your domains**

You can see all domains under Configurations → Object Setup → Cases → Domains. From this tab, you can edit the properties of the built-in domains and create your own custom domains.

Consider the following information:

* You can't merge cases with different domains.
* SmartScore and smart grouping are not supported for custom domains.
*
* For SBAC, use the Cases and Issues scoping area to define case and issue domains that enable you to control access to your domains. For more information, see [Manage user scope](../../onboard-cortex-xsiam/post-deployment/manage-user-roles-and-access-management/manage-user-scope).
* Domains might affect custom content that is connected to cases and issues. Review your custom content to ensure it is associated with the intended domains. This includes:
  * Automation Rules
  * Starring Rules
  * Notifications
  * Issue Exclusions
  * Scoring Rules
  * XQL that accesses the cases or issues datasets in Scheduled Queries and Widgets

### **How to create a case domain**

* Adding custom domains requires a View/Edit RBAC permission for Case Properties (under Object Setup).
* Once created, a custom case domain cannot be deleted or renamed.

1.  Go to Settings → Configurations → Object Setup → Cases → Domains .

    The existing domains are listed.
2. Click on + New Domain.
3. Assign a name and color to the domain, and an optional description.
4. In the Status field, select one or more statuses that are relevant to the domain. These statuses will be available for selection in the cases and issues associated with this domain.
5. In the Resolution Type field, select one or more resolution reasons that are relevant to the domain. These reasons will be available for selection in the cases and issues associated with this domain.
6. Click Save.
7. (Optional) Update SBAC scoping to enable access to the domain.
   1. You can perform the following:
      * To enable access to the domain for a User Group, go to Settings → Configurations → Access Management → User Groups.
      * To enable access to the domain for a User, go to Settings → Configurations → Access Management → Users.
      * To enable access to the domain for an API key, got to Settings → Configurations → Integrations → API Keys.
   2. When editing an existing User Group, User, or API key, in the Scope tab you can update the granular scoping for the new Endpoints domain.
   3. Click Save.

<br>
