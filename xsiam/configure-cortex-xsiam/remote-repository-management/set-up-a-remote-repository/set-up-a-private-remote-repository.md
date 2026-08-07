---
description: Set up the private remote repository feature.
---

# Set up a Private Remote Repository

Before you begin, verify that you have network connectivity from Cortex XSIAM to the private remote repository. All communication goes through Cortex XSIAM, so it must have access to the remote repository. If direct access from Cortex XSIAM is not enabled you can use engines with access to the repository.

{% hint style="info" %}
**TIP**

Due to security concerns, there is a closed allow list of approved URLs for private repositories. If you want to use a URL that is excluded from the allow list, use an engine (engine groups are not supported).
{% endhint %}

The following are typical scenarios for setting up a private remote repository for the production and one or more development tenants.

{% hint style="info" %}
Once enabled, the development push tenant has a red banner on the top left showing DEV.
{% endhint %}

### New development tenant and new or existing production tenant

In this scenario, the production tenant is first activated as a standalone (by default), and the built-in remote repository is then enabled in the production tenant (as a pull tenant). Once enabled, the first development tenant becomes the push tenant and any additional tenants become pull tenants.

Perform the following procedures in the order listed below.

<details>

<summary>Task 1. Enable the private remote repository for the production tenant</summary>

1. In the production tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction is **Pull**.
2. In the **Repository type** field, select **Private**, and save the settings.
3. Define the Git settings using HTTPS or SSH.

{% hint style="info" %}
* For repository vendors that use tokens, enter the token type in the **username** field and the token in the **password** field. Verify details with your vendor.\
  If your private Git remote repository uses personal access tokens instead of usernames and passwords, enter the token type in the **username** field and the access token in the **password** field. For example, if you use an OAuth2 token, enter `oauth2` in the username field. For Github, enter your username in the username field.
* If using SSH, RSA or ed25519 algorithm private keys are supported. If your SSH connection uses a port other than port 22 (the default SSH port), you must include the SSH string and port number in the **Repository URL** field. In the following example, we use port 20017:\
  `ssh://git@content.demisto.com:20017/~/my-project.git`
{% endhint %}

4. Select the active branch on which you will be working.
5. In the **Advanced** section, the engine is set by default. You can change the engine by selecting from the list of available engines.

{% hint style="info" %}
You can't add an engine that has been added to a Load-Balancing Group.
{% endhint %}

</details>

<details>

<summary>Task 2. Activate a new development tenant in Cortex Gateway for a private remote repository</summary>

1. In Cortex Gateway , locate the Cortex XSIAM production tenant where you enabled the private repository in Task 1.
2. Hover over the Cortex XSIAM tenant and click **Activate Dev Tenant**.
3. Define the following fields:

| Name                 | Details                                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEV TENANT NAME      | Give the Cortex XSIAM dev tenant an easily recognizable name. Choose a name that is 59 or fewer characters and is unique across your company account.                                           |
| REGION               | Select the region in which you want to set up the Cortex XSIAM dev tenant.                                                                                                                      |
| DEV TENANT SUBDOMAIN | Give your Cortex XSIAM dev instance an easy-to-recognize name that is used to access the tenant directly using the full URL (**`https://_<subdomain>_xsiam._<region>_.paloaltonetworks.com`**). |

4. Accept the terms and conditions and activate the tenant.

</details>

<details>

<summary>Task 3. Enable the private remote repository in the development tenants</summary>

The first development tenant automatically becomes the push tenant. For more details about push and pull tenants, see [Cortex XSIAM development tenant](../cortex-xsiam-development-tenant).

1. In the development tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction for the first development tenant is **Push**. The sync direction for any additional development tenants is **Pull**.
2. In the **Repository type** field, select **Private**.
3. Define the GitHub settings using HTTPS or SSH.
   1. Select the active branch on which you will be working.\
      You can either use the same branch as for the pull tenant (production or additional development tenant), or a different branch. If using a different branch, you need to define a manual or automatic merge between branches which is done outside Cortex XSIAM.
   2. In the **Advanced** section, the engine is set by default. You can change the engine by selecting from the list of available engines.

{% hint style="info" %}
* If your private Git remote repository uses personal access tokens instead of usernames and passwords, enter the access token in the password field and leave the username field blank.
* For repository vendors that use tokens, the token type is entered in the username field, and the token is entered in the password field. Verify details with your vendor.
* If using SSH, only RSA private keys are supported. If your SSH connection uses a port other than port 22 (the default SSH port), you must include the SSH string and port number in the **Repository URL** field. In the following example, we use port 20017:\
  `ssh://git@content.demisto.com:20017/~/my-project.git`
{% endhint %}

4. Save the settings.
5. Repeat tasks 2 and 3 to enable the private remote repository in each additional development tenant. They will automatically be set to pull.

</details>

### Existing development and production tenants

In this scenario, the production and development tenants were managed in parallel with different sets of content. Since they were already activated in Cortex Gateway, their remote repository settings can only be changed within the tenants.

{% hint style="info" %}
The first tenant that is enabled pushes its content to the remote repository first. For example, these instructions describe enabling the production tenant first, so the remote repository will initially contain production tenant content. You can enable a development tenant first if you want the remote repository to initially contain the content from the development tenant.
{% endhint %}

Perform the following procedures in the order listed below.

<details>

<summary>Task 1. Enable the private remote repository for the production tenant</summary>

1. In the production tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction is **Pull**.
2. In the **Repository type** field, select **Private**, and save the settings.
3. Define the Git settings using HTTPS or SSH.

{% hint style="info" %}
* For repository vendors that use tokens, enter the token type in the username field and the token in the password field. Verify details with your vendor. If your private Git remote repository uses personal access tokens instead of usernames and passwords, enter the token type in the username field and the access token in the password field. For example, if you use an OAuth2 token, enter `oauth2` in the username field. For Github, enter your username in the username field.
* If using SSH, RSA or ed25519 algorithm private keys are supported. If your SSH connection uses a port other than port 22 (the default SSH port), you must include the SSH string and port number in the Repository URL field. In the following example, we use port 20017:\
  `ssh://git@content.demisto.com:20017/~/my-project.git`
{% endhint %}

4. Select the active branch on which you will be working.
5. In the **Advanced** section, the engine is set by default. You can change the engine by selecting from the list of available engines.\
   You can't add an engine that has been added to a Load-Balancing Group.

</details>

<details>

<summary>Task 2. Enable the private remote repository in the development tenants.</summary>

Once enabled, the first development tenant automatically becomes the push tenant. For more details about push and pull tenants, see [Cortex XSIAM development tenant](../cortex-xsiam-development-tenant).

1. In the development tenant, go to **Settings** → **Configurations** → **General** → **Remote Repository Settings** and toggle the **Content repository** slider to enable the remote repository. When set to **On**, the sync direction for the first development tenant is **Push**. The sync direction for any additional development tenants is **Pull**.
2. In the Repository type field, select **Private**.
3. Define the GitHub settings using HTTPS or SSH.
   1. Select the active branch on which you will be working.
   2. In the **Advanced** section, add any engines you want to connect.

{% hint style="info" %}
* If your private Git remote repository uses personal access tokens instead of usernames and passwords, enter the access token in the password field and leave the username field blank.
* For repository vendors that use tokens, the token type is entered in the username field and the token is entered in the password field. Verify details with your vendor.
* If using SSH, only RSA private keys are supported. If your SSH connection uses a port other than port 22 (the default SSH port), you must include the SSH string and port number in the **Repository URL** field. In the following example, we use port 20017:\
  `ssh://git@content.demisto.com:20017/~/my-project.git`
{% endhint %}

4. Select which content to keep and which to overwrite. If there are any discrepancies between the development tenant and remote repository (which in this example initially contains the production tenant content after it is enabled), the **Specified repository is not empty** window opens. Options are:

* **Existing content on your tenant**: Keeps the existing content on your tenant and replaces the content on the specified repository. Cortex XSIAM checks if any other tenants are using the remote repository. If yes, this option is disabled. In this example, the remote repository was already enabled in the production tenant, so the remote repository holds production content. If you want to keep the content on the development tenant:
  1. Disable the remote repository in any additional enabled tenants. In this case, for the first development tenant, only the production tenant must be disabled.
  2. Select **Existing content on your tenant** for this tenant.
  3. Complete synchronization.
  4. Re-enable the remote repository in any additional tenants and select Existing content on the specified repository in each additional tenant.
* **Existing content on the specified repository**: Deletes the existing content on your tenant and replaces it with content from the specified repository.

5. Click **Continue**.

</details>
