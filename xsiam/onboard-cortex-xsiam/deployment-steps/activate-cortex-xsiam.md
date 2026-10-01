---
description: >-
  Activate Cortex XSIAM tenants in Cortex Gateway, including prerequisites,
  encryption, and access configuration.
---

# Activate Cortex XSIAM

To activate a tenant, you need to log in to Cortex Gateway, a centralized portal for activating and managing tenants, users, roles, and user groups. After activating the tenant, you can then access the tenant. You must repeat this task for each tenant if you have multiple tenants. The activation process involves accessing Cortex Gateway, activating the tenant, and then accessing the tenant's resources.

{% hint style="warning" %}
### Prerequisite

You must have the following:

* The Cortex XSIAM activation email.
*   A Customer Support Portal (CSP) account.

    Set up your CSP account. For more information, see [How to Create Your CSP User Account](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000ClNVCA0).

    When you create a CSP account, you can set up two-factor authentication (2FA) to log into the CSP by using an Email, Okta Verify, or Google Authenticator (non-FedRAMP accounts). For more information, see [How to Enable a Third Party IdP](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA14u000000sZ8mCAE).
*   You have the following roles assigned in the CSP:

    | Role        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Super User  | <p>Your Customer Support Portal account must have the Super User role. The user who creates the account receives this role.<br><br>Use this role to sign in to Cortex Gateway for the first time. You then receive the initial Account Admin permissions required to activate the Cortex XSIAM tenant.<br><br>In Cortex Gateway, you can activate new tenants, access existing tenants, and create and manage role-based access control (RBAC) for all your tenants.</p>                                                                    |
    | Cortex User | <p>You must be assigned the <strong>Cortex User</strong> role within the Customer Support Portal to ensure that user synchronization completes successfully during and after the activation process. Without this role assigned, activation fails.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If adding users through the CSP, assign them the Cortex User role; otherwise, they won't appear in the Cortex Gateway or tenant user lists and will be blocked from using the tenant.</p></div> |
{% endhint %}

How to activate Cortex XSIAM

1.  Log in to Cortex Gateway.

    You can also access the link from the activation email.
2.  Enter your username and password or multi-factor authentication (if set up) by using your Customer Support Portal account credentials to sign in.

    After you sign in, you can view the following:

    * If you are a CSP Account Admin, you can see tenants allocated to your CSP account and ready for activation. After activation, you cannot move your tenant to a different CSP account.
    * Tenant details such as license type, number of endpoints, and purchase date.
    * Tenants that were activated and are now available. If you have more than one Customer Support Portal account, the tenants are displayed according to the Customer Support Portal account name.
3.  In the **Available for Activation** section, use the serial number to locate the tenant that needs activation, and then click **Activate**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>When you activate, a production tenant is activated first. After activation, you can set up a development tenant (subject to your license).</p></div>
4.  On the **Tenant Activation** page, define the following:

    | Parameter         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
    | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Tenant Name       | Enter the name of the tenant. Use a unique name across your company account up to 59 characters long.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
    | Region            | Geographic location where your tenant will be hosted. For more information about supported regions, see [Cortex XSIAM supported regions](activate-cortex-xsiam/cortex-xsiam-supported-regions).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    | Tenant Subdomain  | <p>DNS record associated with your tenant. Enter a name that will be used to access the tenant directly using the full URL:</p><p><code>https://&#x3C;subdomain>xdr.&#x3C;region>.paloaltonetworks.com</code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
    | Encryption Method | <p>(Optional) If you want to bring your own keys for encrypting your data, under <strong>Advanced</strong>, select <strong>BYOK</strong> and follow the instructions of the wizard as detailed in <strong>Encryption Method</strong>.</p><ul><li><p>Default encryption (recommended)</p><p>All data stored by Cortex XSIAM is encrypted at rest using a dedicated key management system. Cortex XSIAM provides strict key access controls and auditing, and encrypts user data at rest according to AES-256 encryption standards. We recommend using this default system.</p></li><li><p>BYOK (Bring your own keys)</p><p>BYOK (Bring Your Own Keys) enables you to generate your own encryption keys and securely import and manage them via Cortex Gateway to retain greater control over your tenant data and encryption. This requires <a href="activate-cortex-xsiam/bring-your-own-keys">further setup</a>.</p></li></ul> |
5.  Review and **agree to the terms and conditions of the Privacy policy, Terms of Use, and EULA** , and then **Activate** your tenant.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Activation can take about an hour and does not require you to remain on the activation page. Cortex XSIAM sends a notification to your email when the process is complete.</p></div>
6. After activation, from the Cortex Gateway, in the **Available Tenants**, when hovering over the activated tenant, do the following:
   * Ensure that you can successfully access the tenant by clicking the Cortex XSIAM tenant name (when the tenant is active).
   *   In the dialog box, view the tenant status, region, serial number, and license details.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you want to change your tenant's name, the subdomain, or activate a development tenant (subject to license), on the right-hand side, click the ellipsis.</p><p>You can only change the subdomain once, and it cannot be undone.</p><p>After deleting the subdomain, you can reuse it after 7 days.</p></div>
7. Enable and verify access to Cortex XSIAM communication servers, storage buckets, and various resources in your firewall configuration. For more information, see [Enable access to required PANW resources](https://app.gitbook.com/s/FOhYBYLdbwpnbJgr6uaX/cortex-xdr-3.x-documentation/onboard-and-configure-cortex-xdr/deployment-steps/step-1-activate-cortex-xdr/enable-access-to-required-panw-resources).
