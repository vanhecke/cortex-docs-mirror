---
description: >-
  Set up the Cortex XSIAM built-in remote repository to synchronize content
  between production and development tenants.
---

# Set up a built-in remote repository

Set up the Cortex XSIAM built-in remote repository to manage and synchronize content across production and development tenants. Use the scenarios below to configure push and pull tenant roles.

{% hint style="info" %}
Once enabled, development tenants have a red banner on the top left showing DEV.
{% endhint %}

### Set up a built-in repository for a new development tenant

In this scenario, activate the production tenant as standalone first. Then enable the built-in remote repository in the production pull tenant. The first development tenant becomes the push tenant. Any additional development tenants become pull tenants.

Perform the following procedures in the order listed below.

<details>

<summary>Task 1. Enable the built-in remote repository in the production tenant.</summary>

1. In the production tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction is **Pull**.
2. In the **Repository type** field, select **Built-in**, and save the settings.

</details>

<details>

<summary>Task 2. Activate a Cortex XSIAM development tenant in Cortex Gateway.</summary>

1. In [Cortex Gateway](https://cortex-gateway.paloaltonetworks.com/accounts) , locate the Cortex XSIAM production tenant where you enabled the built-in repository in task 1.
2. Hover over the Cortex XSIAM tenant and click **Activate Dev Tenant**.
3. Define the following fields:

| Name                 | Details                                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEV TENANT NAME      | Give the Cortex XSIAM dev tenant an easily recognizable name. Choose a name that is 59 or fewer characters and is unique across your company account.                                           |
| REGION               | Select the region in which you want to set up the Cortex XSIAM dev tenant.                                                                                                                      |
| DEV TENANT SUBDOMAIN | Give your Cortex XSIAM dev instance an easy to recognize name that is used to access the tenant directly using the full URL (**`https://_<subdomain>_xsiam._<region>_.paloaltonetworks.com`**). |

4. Select ENABLE CONTENT REPOSITORY.
5. Accept the terms and conditions and activate the tenant.
6. Repeat this task to activate any additional development tenants in Cortex Gateway. They will automatically be set to pull.

</details>

### Set up a built-in repository for existing tenants

In this scenario, production and development tenants were managed separately with different content. Because they are already activated in Cortex Gateway, update their remote repository settings within each tenant.

{% hint style="info" %}
The first tenant that is enabled pushes its content to the remote repository first. For example, these instructions describe enabling the production tenant first, so the remote repository will initially contain production tenant content. You can enable a development tenant first if you want the remote repository to initially contain the content from the development tenant.
{% endhint %}

Perform the following procedures in the order listed below.

<details>

<summary>Task 1. Enable the built-in remote repository in the production tenant.</summary>

1. In the production tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction is **Pull**.
2. In the **Repository type** field, select **Built-in**, and save the settings.

</details>

<details>

<summary>Task 2. Enable the built-in remote repository in the development tenants.</summary>

Once enabled, the first development tenant becomes the push tenant automatically. For details about Cortex XSIAM push and pull tenants, see [cortex-xsiam-development-tenant](../cortex-xsiam-development-tenant "mention").

1. In the development tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction for the first development tenant is **Push**. The sync direction for any additional development tenants is **Pull**.
2. In the **Repository type** field, select **Built-in**, and save the settings.
3. Select which content to keep and which to overwrite. If there are any discrepancies between the development tenant and remote repository (which in this example initially contains the production tenant content after it is enabled), the **Specified repository is not empty** window opens. Options are:

* **Existing content on your tenant**: Keeps the existing content on your tenant and replaces the content on the specified repository. Cortex XSIAM checks if any other tenants are using the remote repository. If yes, this option is disabled. In this example, the remote repository was already enabled in the production tenant, so the remote repository holds production content. If you want to keep the content on the development tenant:
  1. Disable the remote repository in any additional enabled tenants. In this case, for the first development tenant, only the production tenant must be disabled.
  2. Select **Existing content on your tenant** for this tenant.
  3. Complete synchronization.
  4. Re-enable the remote repository in any additional tenants and select **Existing content on the specified repository** in each additional tenant.
* **Existing content on the specified repository**: Deletes the existing content on your tenant and replaces it with content from the specified repository.

4. Click **Continue**.

</details>
