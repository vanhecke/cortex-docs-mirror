---
description: >-
  Install Cortex Marketplace content packs, review dependencies, and configure
  integrations and data sources in Cortex XSIAM.
---

# Install content packs

You can only install one content pack at a time. Cortex XSIAM automatically adds any content that is required to install the content pack. You can also add any optional content packs that use the content pack you want to install.

If you receive an error message when you try to install a content pack, you need to fix the error before installing. If a warning message is issued, you can still download the content pack, but you should fix the problem; otherwise, the content may not work correctly.

Before you install a content pack, you should review the content pack to see what it includes and what the various dependencies are. The following is the information you can view:

* **Details:** General information about the content pack such as installation, content, version, author, and status.
* **Content:** The content to be installed, such as scripts or integrations.
* **Dependencies:** Details of any required content packs and optional content packs that may need to be installed with your content pack.
* **Version History:** View the currently installed version, earlier versions, available updates, and revert if required.

If you want to install data sources, you can do one of the following:

* Go to the **Data Sources & Integrations** page and add a data source. Once configured, it automatically installs the required content packs and recommends additional beneficial content such as playbooks and dashboards that are relevant for this specific data source.
* In Marketplace, select either Data Onboarder (which takes you to the integration configuration in the **Data Sources & Integrations** page) or install the content pack directly from Marketplace. If installing the content pack from Marketplace, you will then have to configure the integration in the **Data Source & Integrations** page.

{% hint style="info" %}
Currently, not all content packs are supported in the **Data Sources & Integrations** page. For example, content packs with several integrations are not yet supported.
{% endhint %}

How to install a content pack in Marketplace

1. Go to Settings → **Configurations** → **Marketplace** → **Browse** and locate the content pack you want to install.
2. Click the required content pack and review the contents.
3. Click **Install** to add the content pack to the **Cart**.
4.  (Optional) If the content pack includes optional content, select the content packs you want to add.

    The **Cart** displays the number of items you are installing, including any required content packs. You can log in and out, but the content packs remain in the **Cart** until you click either **Empty cart** or **Install**.
5. Click **Install**.
6.  After installation, click **Refresh content**.

    You can now start configuring your content. If you have installed an integration, configure the integration, including setting up an integration instance.

{% hint style="info" %}
Content packs are also automatically installed when you adopt playbooks and configure tasks.
{% endhint %}
