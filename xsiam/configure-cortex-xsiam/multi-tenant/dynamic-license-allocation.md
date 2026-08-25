---
description: >-
  Dynamically allocate Cortex XSIAM licenses, endpoints, employees, and storage
  across child tenants in centrally managed multi-tenant deployments.
---

# Dynamic license allocation

In a multi-tenant environment with central licensing management, in Cortex Gateway you can edit child tenant allocations, add child tenants, and delete child tenants. When you delete a child tenant, the tenant's allocations of endpoints, employees, and GBs are returned to the main account's pool and can immediately be used for existing child tenants or for creating new child tenants.

<details>

<summary>Edit tenant allocations in Cortex XSIAM</summary>

You can edit the child tenant allocations by increasing or decreasing the amount of endpoints, employees, and GBs allocated to the tenant. The total available count for the multi-tenant environment is updated accordingly.

{% hint style="info" %}
### Note

Changing the tenant's allocations might result in a short downtime of your tenant.
{% endhint %}

1. In Cortex Gateway, locate the main account and then hover over the child tenant until the three-dot menu appears and click **Edit Tenant Allocations**.
2. In the **Edit Tenant Allocations** window, assign the number of Gigabytes and endpoints you want to allocate to this child tenant. The amount used and the total amount available to this multi-tenant environment are displayed. Ensure you meet the [minimum allocation requirements](onboard-cortex-multi-tenant/onboarding-checklist-for-multi-tenant-central-licensing-deployments/step-2.-create-a-child-tenant). Click **Done**.

</details>

<details>

<summary>Add a child tenant in Cortex XSIAM</summary>

When you have enough license allocations available in your multi-tenant central licensing environment, you can add a child tenant to the main account in Cortex Gateway.

1. In the Cortex Gateway, hover over the main account you activated previously until the three-dot menu appears and click **Add Child Tenant**.
2.  Add the following details:

    | Parameter              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
    | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Child Tenant Name      | <p>Give the Cortex XSIAM tenant an easily recognizable name.</p><p>Choose a name that is 59 or fewer characters and is unique across your company account.</p>                                                                                                                                                                                                                                                                                                                                                          |
    | Region                 | View the region for the child tenant.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
    | Child Tenant Subdomain | <p>Give your Cortex XSIAM instance an easy-to-recognize name that is used to access the tenant directly using the full URL.</p><p>https://&#x3C;subdomain>.crtx.&#x3C;region>.paloaltonetworks.com</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>This is a public FQDN, so be careful with sensitive information such as the company name.</p><p>After activating a child tenant, you can only change the child tenant subdomain once.</p></div> |
    | Child Units Allocation | <p>Assign the number of employees and Gigabytes you want to allocate to this child tenant. The amount used and the total amount available to this multi-tenant environment are displayed.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Ensure that you meet the minimum requirements for child tenant allocation.</p></div>                                                                                                                     |
    | Add Ons                | If any license add-ons were purchased with your multi-tenant license, they are listed here. If you acquired compute units (CU) or forensics, you can allocate how many units to allocate to this child tenant.                                                                                                                                                                                                                                                                                                          |
3.  Confirm approval of the terms and conditions of the privacy policy and click **Activate**.

    Activation can take up to an hour. You should receive notification by email that the child tenant has completed the activation process.
4.  (Optional) Add another child tenant by repeating steps 1 and 2 or access your newly created tenant.

    In the Cortex Gateway, under your main account, you can see the total number of tenants you are licensed for and how many you have created.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you reach your limit for child tenants, depending on your license, you may be able to create more tenants. You may be charged for additional tenants. Contact Customer Support if you are approaching your authorized limit.</p></div>

</details>

<details>

<summary>Delete a child tenant in Cortex XSIAM</summary>

Deleting a child tenant deletes all of its data and content permanently. The child tenant's license allocations are returned to the total available in the multi-tenant environment and can be allocated to other child tenants.

{% hint style="info" %}
### Note

In a multi-tenant central licensing management environment, you cannot unpair a child tenant from the main account. The only way to remove the connection to the main account is to delete the tenant.
{% endhint %}

1. In Cortex Gateway, locate the main account and then hover over the child tenant until the three-dot menu appears and click **Delete Tenant**.
2. In the **Delete Tenant** window, confirm that you want to delete the child tenant by typing 'Delete' and click **Confirm Deletion**.

</details>
