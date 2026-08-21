---
description: >-
  Authenticate Cortex XSIAM users through Customer Support Portal and assign
  Gateway or tenant access roles.
---

# Authenticate users through the Customer Support Portal

When you add users to your Customer Support Portal account, users are sent an invitation to join. After they accept, users can access Cortex Gateway and tenants, but they cannot view any tenants in the Gateway and cannot view any data in the tenant unless they are assigned a direct role or user group role. Only Account Admins can make any changes in Cortex Gateway.

**Keep in mind the following**:

* You must be assigned the Super User role in the Customer Support Portal to add users in the Customer Support Portal.
* The first Super User who logs into Cortex Gateway is automatically assigned the Account Admin role and has access to the tenant. The user who activates the Cortex XSIAM tenant will also be assigned the Account Admin role (if there is no current Account Admin role) or Instance Admin (if there is an existing Account Admin role) and will have access to the tenant. Any additional users including Super Users need to be assigned access to the tenant.
* To log in to Cortex XSIAM through the Customer Support Portal (CSP), users must be assigned the Cortex User role in CSP. If this role is not assigned, the user will be unable to log in via the CSP and must use the Single Sign-On (SSO) login method instead.

When users log into Cortex Gateway or the tenant they are prompted to sign into the Customer Support Portal using their username and password. This is the default method of authentication.

{% hint style="info" %}
After users are added to the Customer Support Portal and they accept the invitation, you can manage them in Cortex Gateway or the Cortex XSIAM tenant.
{% endhint %}

How to authenticate users through the Customer Support Portal

{% stepper %}
{% step %}
### Add the user to your Customer Support Portal.

Sign in to the [Customer Support Portal](https://support.paloaltonetworks.com/) and do one of the following:

* **Create a user**
  1. Select **Members** → **Create New User**.
  2.  Add the member details and click **Submit**.

      The user must accept the email invitation within seven days.

      For invitation help, see [How a Super User Creates a New Customer Support Portal User Account](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000ClNPCA0).
* **Send an account registration link**
  1. Select **Account Management** → **Account Details** → **User Access**.
  2. In **Account Registration**, click **Create**.
  3.  Copy and send the link to the user.

      The user submits their registration details through the link. The Super User receives a creation notification.

      For link management, see [How to Use the Account Registration Link](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000ClNXCA0).
{% endstep %}

{% step %}
### Wait for the user to accept

The user accepts the invitation. They can then sign in to Cortex Gateway.
{% endstep %}

{% step %}
### Assign tenant access

In Cortex Gateway or the Cortex XSIAM tenant, assign a role directly. Alternatively, add the user to a user group with a role.
{% endstep %}
{% endstepper %}
