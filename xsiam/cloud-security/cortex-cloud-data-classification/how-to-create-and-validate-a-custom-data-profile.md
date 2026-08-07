# How to create and validate a custom data profile

{% hint style="info" %}
This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on. If you have the Endpoint DLP add-on, Data Classification is automatically available.
{% endhint %}

### Overview

A data profile is a label which is applied to a data object such as a file or table and defines a data-related business case.

Data profiles are a fundamental component of your organization's data security strategy, serving as the vehicle that defines what is considered sensitive data. Data profiles specifically outline the sensitive data your organization aims to discover, monitor, or receive alerts about. Profiles can be applied to and calculated for various data sources, including files, tables, and text-based information such as API calls.

You can create data profiles to customize sensitive data definitions according to your requirements, complementing or extending the predefined out-of-the-box (OOTB) profiles.

### Understand custom data profiles

Unlike OOTB profiles, which are fixed lists and cannot be edited or erased, custom data profiles offer full flexibility: they can be edited, duplicated, deleted, disabled, or enabled. This means you can either build a custom profile from scratch, or start by duplicating an existing OOTB profile and then modifying it. When you duplicate an OOTB profile, the system initially assigns it a name "copy of X," but you can rename it as required.

### Create a new custom data profile

When creating a custom data profile, you need to define various parameters that specify what constitutes sensitive data.

1. In the lower left part of the screen, click **Settings** → **Configurations**.
2. In the **Configurations** column, under **Data Classification**, click **Data Profiles**.
3. On the **Data Profiles** screen, click **+ Add Profile**.
4.  On the **Create New Data Profile** screen, do the following:

    1. In the **Data Profile Name** field, specify a data profile name. To add an optional description, click **Add description** and enter a description in the text box that opens. If you change your mind and want to remove it, click **Remove description**.
    2. Under **Select Data Location**, select the locations that you want to assign to your new data profile:
       * **Cloud**: includes a variety of parameters.
       * **Endpoints**: Includes only data patterns.
       * **APIs:** Includes only data patterns.
    3. Under **Set Conditions**, select the filters you want to set for your new data profile.
       * **Cloud**: Includes a variety of filters.
       * **Endpoints**: Includes only data patterns.
       * **APIs**: Includes only data patterns.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you choose two data locations, only the filters they have in common will be included in the possible filter options.</p></div>
5.  Click **Create**.

    The new custom data profile now appears in the **Data Profiles** list.

### Manage custom data profiles

You can manage custom data profiles as follows:

* **Edit:** You can fully edit any custom profile.
* **Duplicate:** All custom profiles can be duplicated using the context menu in the **Data Profiles** list.
*   **Delete:** Only custom data profiles can be deleted using the context menu in the Data Profiles list.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>Deleting a data profile deletes all past data associated with it in all modules using Cortex Cloud Data Classification after a warning notification is displayed.</p></div>
*   **Enable or Disable:** You can enable or disable any data profile, custom or OOOB.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>Enabling and disabling a data profile removes or re-adds the data profile results to the data objects; that is, files and tables.</p></div>

### Enable and disable data profiles

{% hint style="info" %}
### Note

For more information, see [How to disable and enable data profiles in Cortex Cloud Data Classification](how-to-disable-and-enable-data-profiles-in-cortex-cloud-data-classification).
{% endhint %}
