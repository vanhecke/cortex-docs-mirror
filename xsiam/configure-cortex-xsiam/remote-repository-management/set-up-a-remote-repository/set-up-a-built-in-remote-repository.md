---
description: >-
  Set up the built-in remote repository feature for production and development
  tenants.
---

# Set up a built-in remote repository

The following are typical scenarios for setting up a built-in remote repository for the production and one or more development tenants.

{% hint style="info" %}
Once enabled, development tenants have a red banner on the top left showing DEV.
{% endhint %}

### New development tenant and new or existing production tenant

In this scenario, the production tenant is first activated as a standalone (by default), and the built-in remote repository is then enabled in the production tenant (as a pull tenant). Once enabled, the first development tenant becomes the push tenant and any additional tenants become pull tenants.

Perform the following procedures in the order listed below.

<details>

<summary>Task 1. Enable the built-in repository in the production tenant.</summary>

1. In the production tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction is **Pull**.
2. In the **Repository type** field, select **Built-in**, and save the settings.

</details>

<details>

<summary>Task 2. Activate a new development tenant in Cortex Gateway for a built-in repository.</summary>

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

### Existing development and production tenants

In this scenario, the production and development tenants were managed in parallel with different sets of content. Since they were already activated in Cortex Gateway, their remote repository settings can only be changed within the tenants.

{% hint style="info" %}
The first tenant that is enabled pushes its content to the remote repository first. For example, these instructions describe enabling the production tenant first, so the remote repository will initially contain production tenant content. You can enable a development tenant first if you want the remote repository to initially contain the content from the development tenant.
{% endhint %}

Perform the following procedures in the order listed below.

<details>

<summary>Task 1. Enable the built-in repository in the production tenant.</summary>

1. In the production tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction is **Pull**.
2. In the **Repository type** field, select **Built-in**, and save the settings.

</details>

<details>

<summary>Task 2. Enable the built-in remote repository in the development tenants.</summary>

Once enabled, the first development tenant automatically becomes the push tenant. For more details about push and pull tenants, see [Cortex XSIAM development tenant](../cortex-xsiam-development-tenant).

1. In the development tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction for the first development tenant is **Push**. The sync direction for any additional development tenants is **Pull**.
2. In the **Repository type** field, select **Built-in**, and save the settings.
3. Select which content to keep and which to overwrite. If there are any discrepancies between the development tenant and remote repository (which in this example initially contains the production tenant content after it is enabled), the **Specified repository is not empty** window opens. Options are:

* **Existing content on your tenant**: Keeps the existing content on your tenant and replaces the content on the specified repository. Cortex XSIAM checks if any other tenants are using the remote repository. If yes, this option is disabled. In this example, the remote repository was already enabled in the production tenant, so the remote repository holds production content. If you want to keep the content on the development tenant:
  1. Disable the remote repository in any additional enabled tenants. In this case, for the first development tenant, only the production tenant must be disabled.
  2. Select **Existing content on your tenan**t for this tenant.
  3. Complete synchronization.
  4. Re-enable the remote repository in any additional tenants and select **Existing content on the specified repository** in each additional tenant.
* **Existing content on the specified repository**: Deletes the existing content on your tenant and replaces it with content from the specified repository.

4. Click **Continue**.

</details>
