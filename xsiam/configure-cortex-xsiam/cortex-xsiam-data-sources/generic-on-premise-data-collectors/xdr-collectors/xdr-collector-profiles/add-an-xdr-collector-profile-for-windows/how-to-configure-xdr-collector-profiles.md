---
description: Configure XDR Collector profiles for Cortex XSIAM.
---

# How to configure XDR Collector profiles

{% hint style="info" %}
**Note**

Ingestion of log events larger than 5 MB is not supported.
{% endhint %}

<details>

<summary><strong>Filebeat configuration</strong></summary>

In the **Filebeat Configuration File** editor, you can define the data collection for your Elasticsearch Filebeat configuration file called `filebeat.yml`.

Cortex XSIAM provides YAML templates for DHCP, DNS, IIS, XDR Collector Logs, NGINX, and any templates added by the content packs installed from the XSIAM Marketplace.

1. Select **Settings** → **Configurations** → **XDR Collectors** → **Profiles** → **+Add Profile** → **Windows**.
2. Select **Filebeat**, then click **Next**.
3. Configure the **General Information** parameters.
   * **Profile Name**: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) **Add description here**: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4. In the **Filebeat Configuration File** editing box, type or paste the contents of your configuration file, or use a template. To add a template, select one from the list, and click **Add**.
5.  Cortex XSIAM supports all sections in the `filebeat.yml` configuration file, such as support for Filebeat fields and tags. You can use the "Add fields" processor to identify the product/vendor for the data collected by the XDR Collectors, so that the collected events go through the ingestion flow (Parsing Rules). To configure the product/vendor, ensure that you use the default `fields` attribute (do not use the **target** attribute), as shown in the following example:

    ```
    processors:
      - add_fields:
          fields:
            vendor: <Vendor>
            product: <Product>
    ```

    For more information about the "Add fields" processor, see [Add\_fields](https://www.elastic.co/guide/en/beats/filebeat/current/add-fields.html).
6.  To finish creating your new profile, click **Create**.

    Your new profile will be listed under the applicable platform on the **XDR Collectors Profiles** page.
7. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select **Create a new policy rule using this profile**.
   * Launch the new policy wizard from **XDR Collectors** → **Policies** → **XDR Collectors Policies**.

</details>

<details>

<summary><strong>Winlogbeat configuration</strong></summary>

In the **Winlogbeat Configuration File** editor, you can define the data collection for your Elasticsearch Winlogbeat configuration file called `winlogbeat.yml`.

Cortex XSIAM provides YAML templates for Windows Security, and any templates added by the content packs installed from the XSIAM Marketplace. To add a template, select it and click **Add**.

1. Select **Settings** → **Configurations** → **XDR Collectors** → **Profiles** → **+Add Profile** → **Windows**.
2. Select the **Winlogbeat** profile, then click **Next**.
3. Configure the **General Information** parameters.
   * **Profile Name**: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) **Add description here**: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4. In the **Winlogbeat Configuration File** editing box, type or paste the contents of your configuration file, or use the template. To add the template, click **Select template**, and then click **Windows Security**. Click **Add**.
5.  Cortex XSIAM supports all sections in the `winlogbeat.yml` configuration file, such as support for Winlogbeat fields and tags. You can use the "Add fields" processor to identify the product/vendor for the data collected by the XDR Collectors, so that the collected events go through the ingestion flow (Parsing Rules). To configure the product/vendor, ensure that you use the default `fields` attribute (do not use the `target` attribute), as shown in the following example:

    ```
    processors:
      - add_fields:
          fields:
            vendor: <Vendor>
            product: <Product>
    ```

    For more information about the "Add fields" processor, see [Add\_fields](https://www.elastic.co/guide/en/beats/filebeat/current/add-fields.html).
6.  To finish creating your new profile, click **Create**.

    Your new profile will be listed under the applicable platform on the **XDR Collectors Profiles** page.
7. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select **Create a new policy rule using this profile**.
   * Launch the new policy wizard from **XDR Collectors** → **Policies** → **XDR Collectors Policies**.

</details>

<details>

<summary><strong>Settings configuration</strong></summary>

You can configure automatic upgrades for XDR Collector releases. By default, this is disabled, and the **Use Default (Disabled)** option is selected. To implement automatic upgrades, follow these steps:

1. Select **Settings** → **Configurations** → **XDR Collectors** → **Profiles** → **+Add Profile** → **Windows**.
2. Select **Settings profile**, then click **Next**.
3. Configure the **General Information** parameters.
   * **Profile Name**: Enter a unique name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name that you enter here will be displayed in the list of profiles when you configure a policy.
   * (Optional) **Add description here**: To provide additional context for the purpose or business reason for your new profile, enter a profile description.
4. Clear the **Use Default (Disabled)** checkbox.
5.  For **Collector Auto-Upgrade**, select **Enabled**.

    Additional fields are displayed for defining the scope of the automatic upgrade.
6. Configure the scope of automatic upgrades:
   * To ensure the latest XDR Collector release is used, leave the **Use Default (Latest collector release)** checkbox selected.
   * To configure only a particular scope, perform the following steps:
     1. Clear the **Use Default (Latest collector release)** checkbox.
     2.  For **Auto Upgrade Scope**, select one of the following options:

         | Option                                          | More details                                                                                                                                                                                                      |
         | ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
         | Latest collector release                        | Configures the scope of the automatic upgrade to whenever a new XDR Collector release is available including maintenance releases and new features.                                                               |
         | Only maintenance release                        | Configures the scope of the automatic upgrade to whenever a new XDR Collector maintenance release is available.                                                                                                   |
         | Only maintenance releases in a specific version | Configures the scope of the automatic upgrade to whenever a new XDR Collector maintenance release is available for a specific version. When this option is selected, you can select the specific Release Version. |
7.  To finish creating your new profile, click **Create**.

    Your new profile will be listed under the applicable platform on the **XDR Collectors Profiles** page.
8. Apply profiles to XDR Collector machine policies by performing one of the following:
   * Right-click a profile, and select **Create a new policy rule using this profile**.
   * Launch the new policy wizard from **XDR Collectors** → **Policies** → **XDR Collectors Policies**.

</details>
