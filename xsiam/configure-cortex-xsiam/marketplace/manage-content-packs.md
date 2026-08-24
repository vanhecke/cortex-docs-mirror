---
description: Install, update, revert, and delete Cortex XSIAM Marketplace content packs.
---

# Manage content packs

You can install, delete, update, and revert content packs. Before you install a content pack, you should review the content pack to see what it includes and the various dependencies. The following is the information you can view:

* **Details:** General information about the content pack such as installation, content, version, author, and status.
* **Content:** The content to be installed, such as scripts or integrations.
* **Dependencies:** Details of any required content packs and optional content packs that may need to be installed with your content pack.
* **Version History:** View the currently installed version, earlier versions, available updates, and revert if required.

**Dependencies**

In Cortex XSIAM content packs, some objects are dependent on other objects. For example, an issue may be dependent on a playbook, an issue type, and an issue field. A script may be dependent on another script, or an integration. When you place a content pack in your cart, mandatory dependencies including required content packs are added automatically to ensure that the content pack installs correctly.

Optional content packs are used by the content pack you want to install, but are not necessary for installation. When you place a content pack in your cart, you can choose which optional content pack to install. When you install optional content packs, mandatory dependencies in the optional content pack are automatically included.

{% hint style="info" %}
### Note

Optional content packs that are already installed are treated like they are required content packs to preserve content integrity.
{% endhint %}

<details>

<summary>Install a content pack</summary>

You can only install one content pack at a time. Cortex XSIAM automatically adds any content that is required to install the content pack. You can also add any optional content packs that use the content pack you want to install.

If you receive an error message when you try to install a content pack, you need to fix the error before installing. If a warning message is issued, you can still download the content pack, but you should fix the problem; otherwise, the content may not work correctly.

{% hint style="info" %}
### Note

Cortex XSIAM includes a built-in default mail sender. You also have the option of installing a different mail sender content pack, such as [Microsoft Exchange Online](https://cortex.marketplace.pan.dev/marketplace/details/MicrosoftExchangeOnline/).
{% endhint %}

1. Go to Settings → **Configurations** → **Marketplace** → **Browse** and locate the content pack you want to install.
2. Click the required content pack and review the contents.
3. Click **Install** to add the content pack to the **Cart**.
4.  (Optional) If the content pack includes optional content, select the content packs you want to add.

    The **Cart** displays the number of items you are installing, including any required content packs. You can log in and out, but the content packs remain in the **Cart** until you click either **Empty cart** or **Install**.
5. Click **Install**.
6. After installation, click **Refresh content**.

{% hint style="info" %}
### Note

In addition to content packs that you install from Marketplace, related content packs are automatically downloaded when you adopt playbooks or edit tasks that require content items such as scripts or integrations.
{% endhint %}

</details>

<details>

<summary>Update a content pack</summary>

Content packs are updated for bug fixes, enhancements, and more. Marketplace is updated every 2 hours and when there is an update available for a content pack, you will see a notification in the **Installed Content Packs** tab in Marketplace.

In the **Version History** tab of a content pack, you can see the currently installed version, earlier versions, and available updates. You can revert to a previous version of a content pack if required.

All dependent content packs update automatically with the content pack.

{% hint style="info" %}
### Tip

You can also find content packs that require updates by going to **Settings** → **Data Sources & Integrations** and filtering by **Pack Version** = **Update Available**. If you click on an integration in the filtered list, there is a link to the content pack in Marketplace for updates.
{% endhint %}

{% hint style="info" %}
### Note

Third-party product integrations are developed and tested against a specific product version. For products that are on-prem or cloud-based with specific API versions, the version developed and tested against will be included in the integration's documentation. Newer versions of the product are not always immediately tested, and it is expected that products maintain API compatibility upon release of newer product versions. When upgrading to a newer product version, it is highly recommended to test the integration in a dev environment before deploying to production.
{% endhint %}

{% hint style="warning" %}
### Caution

If you want to downgrade, any content that depends on the content pack including any customizations may be deleted if it does not exist in the target content pack version.
{% endhint %}

1. In the **Show** field of the **Installed Content Packs** tab, select **Update available** to display the content packs that are available to update.
2. Click the content pack you want to update.
3. In the **Version History** tab of the content pack, view the available updates.
4.  Click **Update**. If there is more than one update available, click the version to update.

    If you choose to install the latest version it includes the previous version. If you have made any customizations these are included in any update. If any dependencies require updating, these are automatically added.
5. Click **Install**.
6. After the content pack installs, click **Refresh content**.

</details>

<details>

<summary>Revert a content pack</summary>

You can revert to an earlier version of an installed content pack. Items that are not included in the version are also deleted, such as detached playbooks or scripts that use other scripts from the content pack. This may cause other content packs to stop working

1. In the **Installed Content Packs** tab, click the content pack you want to revert.
2. In the **Version History** tab, select the version to which you want to revert.
3. Click **Revert to this version**. The version will be added to your **Cart**.
4. In the **Cart**, click **Downgrade**.

</details>

<details>

<summary>Delete a content pack</summary>

When you delete a content pack, all content is deleted, including all detached and customized content.

{% hint style="warning" %}
### Caution

If another content pack is dependent on the content pack you want to delete, it may break the other content pack. You can reinstall the content pack, but you cannot restore detached and customized content.
{% endhint %}

1. Go to Settings → **Configurations** → **Marketplace** → **Installed Content Packs**.
2. In the **Content Packs Library** section, search for the content pack and select the content pack you want to delete.
3. Click the trash can icon.
4. Review the warning message and click **Delete**.

</details>
