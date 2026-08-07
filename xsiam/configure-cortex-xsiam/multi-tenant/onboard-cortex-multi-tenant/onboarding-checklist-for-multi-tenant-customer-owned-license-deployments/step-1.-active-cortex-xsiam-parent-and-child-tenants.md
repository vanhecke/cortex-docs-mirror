# Step 1. Active Cortex XSIAM (parent and child tenants)

To set up Cortex XSIAM multi-tenant in a customer-owned license deployment, you need to activate the parent and child tenants in Cortex Gateway. Cortex Gateway is a centralized portal for activating and managing tenants, users, roles, and user groups. After activating the tenants you can then access the tenant. You will need to repeat this task for each tenant if you have multiple tenants. The activation process includes accessing Cortex Gateway, activating the tenant, and then accessing the tenant.

Before you begin, make sure you have the following:

* Cortex XSIAM activation email.
*   Customer Support Portal Super User role is assigned to your account.

    Before activating your Cortex XSIAM tenant, you need to set up your Customer Support Portal account. See [How to Create Your Customer Support Portal User Account](https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000ClNVCA0). When you create a Customer Support Portal account you can set up two-factor authentication (2FA) to log into the Customer Support Portal, by using one of the following:

    * Email
    * Okta Verify
    * Google Authenticator (non-FedRAMP accounts)

    Users who create the Customer Support Portal account are granted the Super User role. If you are the first user to access Cortex Gateway with the Customer Support Portal Super User role, you are automatically granted Account Admin permissions for the gateway.

    You can activate Cortex XSIAM new tenants, access existing tenants, and create and manage role-based access control (RBAC) for all of your tenants.

How to activate Cortex XSIAM

1. Enable and verify access to Cortex XSIAM communication servers, storage buckets, and various resources in your firewall configuration. For more information, see [Enable access to required PANW resources](../../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam).
2.  Go to [Cortex Gateway](https://cortex-gateway.paloaltonetworks.com/signin/) .

    You can also access the link from the activation email.
3.  Enter your username and password or multi-factor authentication (if set up) by using your Customer Support Portal account credentials to sign in.

    Once signed in, you can view the following:

    * Tenants that are allocated to your Customer Support Portal account and ready for activation. After activation, you cannot move your tenant to a different Customer Support Portal account.
    * Tenant details such as license type, number of endpoints, and purchase date.
    * Tenants that were activated and are now available. If you have more than one Customer Support Portal account, the tenants are displayed according to the Customer Support Portal account name.
4. In the Available for Activation section, use the serial number to locate the tenant that needs activation, and then click Activate.
5. On the Tenant Activation page, define the following:
   * Tenant Name: Enter a name for the tenant. Use a name that is unique across your company account and up to 59 characters long.
   * Region: Geographic location where your tenant will be hosted. For more information, see [Cortex XSIAM supported regions](../../../../onboard-cortex-xsiam/deployment-steps/activate-cortex-xsiam).
   *   Tenant Subdomain: DNS record associated with your tenant. Enter a name that will be used to access the tenant directly using the full URL:

       `https://<xsiam-tenant>.xdr.<region>.paloaltonetworks.com`
   *   (Optional) If you want to bring your own keys for encrypting your data, under Advanced, select BYOK and follow the instructions of the wizard as detailed in Encryption Method.

       Encryption Method

       Cortex XSIAM enables you to select the method used to encrypt your tenant data at rest. You can select the encryption method of your tenant only when creating new tenants. Select the encryption method in Advanced → Encryption Method.

<details>

<summary>Default encryption (recommended)</summary>

All data stored by Cortex XSIAM is encrypted at rest using a dedicated key management system. Cortex XSIAM provides strict key access controls and auditing, and encrypts user data at rest according to AES-256 encryption standards. We recommend all our customers use this default system.

</details>

<details>

<summary>BYOK (Bring your own keys)</summary>

BYOK (Bring Your Own Keys) enables you to generate your own encryption keys and securely import and manage them via Cortex Gateway to retain greater control over your tenant data and encryption. This requires [further setup](https://docs-cortex.paloaltonetworks.com/access?ft:originId=UUID-f87e1680-f4d1-fa01-c156-b1e48cf23398\&ft:sourceId=Paligo).

</details>

6. Select I agree to the terms and conditions of the Privacy policy.
7.  Click Activate.

    The activation process can take about an hour and does not require that you remain on the activation page. Cortex XSIAM sends a notification to your email when the process is complete.
8. After activation, from Cortex Gateway, in the Available Tenants when hovering over the activated tenant, do the following:
   * Ensure that you can successfully access the tenant by clicking the Cortex XSIAM tenant name (when the tenant is active).
   * In the dialog box, view the tenant status, region, serial number, and license details.

<br>
