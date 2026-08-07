---
description: >-
  Classify and map extracted values to the appropriate indicator types and
  fields.
---

# Indicator classification and mapping

The following table shows methods by which indicators are detected and ingested in Cortex XSIAM and how they are classified and mapped.

| Method               | Description                                                                                                                                                                        | Classification and Mapping                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Integration          | Feed integrations: Fetch indicators from a feed, for example, TAXII, Office 365, and Unit 42.                                                                                      | <p>Indicator classification and mapping is done in the integration code by duplicating the integration and not in the <strong>Indicators</strong> → <strong>Classification &#x26; Mapping</strong> tab. For more information, see <a href="https://xsoar.pan.dev/docs/integrations/feeds">Feed Integrations</a>.</p><p>Some integrations come with a classifier and mapper, which you can customize.</p> |
| Indicator extraction | If you have enabled system-wide indicator extraction, indicators are extracted from all issues in Cortex XSIAM.                                                                    | Only the value of an indicator is extracted, so no classification or mapping is needed.                                                                                                                                                                                                                                                                                                                  |
| Manual               | <ul><li>Command line</li><li>Mark: The user marks a piece of data as an indicator.</li><li>STIX file: Manually upload a STIX file on the Threat Intel (Indicators) page.</li></ul> | <p>Data is inserted manually via the UI so no classification or mapping is needed.</p><p>If importing an STIX file, mapping is done via the STIX parser code.</p>                                                                                                                                                                                                                                        |

**Classify and map an indicator type for an integration**

The indicator classification and mapping feature enables you to take the data that Cortex XSIAM ingests from integrations, and classify and map the data to indicator types and indicator fields. By classifying the data as different indicator types, you can process them with different playbooks suited to their respective requirements.

{% hint style="info" %}
### Note

When creating a new indicator type, you classify and map the indicator fields in the indicator type settings. For more details, see [Map custom indicator fields](#UUID-c62ed734-e8dd-d01c-8a8f-91546a16d09a).
{% endhint %}

Classification determines the type of indicator that is created for data ingested from a specific integration. You create a classifier and define that classifier in an integration.

You can map the fields from your third-party integration to the fields in your indicator layouts as follows:

* Map your fields to indicator types irrespective of the integration or classifier. This means that you can create a mapping before defining an instance and ingesting indicators. By doing so, when you do define an instance and apply a mapper, the data that comes in is already mapped.
* Create default mapping for all of the fields that are common to all indicator types. You can still overwrite the contents of a field in the specific indicator type.

<details>

<summary>Classify an indicator type</summary>

When an integration fetches indicators, it populates the raw JSON object for the indicator. The raw JSON object contains all of the attributes (fields) for an indicator. For example, source, when the event was created, the priority that was designated by the integration, and more. When classifying ingested indicator data, you want to select an attribute (field) that can determine the indicator type.

Use this procedure to create a classifier or duplicate an existing classifier for ingested indicator data.

1. Select Settings → **Configurations** → **Object Setup** → **Indicators** → **Classification & Mapping**.
2. Do one of the following:
   1. To create a new classifier, select + New → **Indicator Classifier**.
   2.  To edit an existing classifier, select it and click **Edit**.

       If the classifier is installed from a content pack, you need to duplicate and then edit.
3.  Under **Get data**, select from where you want to import the indicator data. You will classify the indicator type based on this information.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>You can optionally skip importing data. Click the pencil on the right of each indicator type on the right pane to enter the value manually.</p></div>

    * **Pull from instance:** Select an existing integration instance to import indicator data from.
    * **Upload JSON:** Upload a formatted JSON file that includes the fields you want to classify by.
4.  Under **Fetched data**, select from the attributes (fields) in the imported indicator object a field that will serve as the classifier (key) to route to a specific indicator type.

    Cortex XSIAM searches through the imported indicator objects for the values for the field you select.
5. Drag the found values from the **Unmapped Values** column to the relevant indicator type on the right pane.
6. **Save** the classifier.
7. Apply the indicator classifier to the relevant feed integration.
   1. Navigate to Settings → **Data Sources & Integrations**.
   2. Select an existing integration instance you want to apply the indicator classifier to or create a new integration instance.
   3. In the integration instance settings under **Classifier**, select the classifier you created and click **Save**.

</details>

<details>

<summary>Map indicator fields</summary>

Mappers enable you to map the information from ingested indicator data to the indicator fields that you have in your system.

Mapping data takes place in two stages:

1. Map all of the fields that are common to all indicators in the default mapping.
2. Map the additional fields that are specific for each indicator type, or overwrite the mapping that you used in the default mapping.

{% hint style="info" %}
### Note

In the **Classification & Mapping** page, the mapping does not indicate for which indicator types they are configured. When creating a mapper, it is best practice to add to the mapper name and the indicator type the mapper is for. For example, Mail Listener - Phishing.

When mapping a list, we recommend you map to a multi-select field. Short text fields do not support lists. If you need to map a list to a short text field, add a transformer in the relevant playbook task to split the data back into a list.
{% endhint %}

Use this procedure to create a mapper or duplicate an existing mapper to map all of the ingested indicator fields to an indicator layout.

1. Select Settings → **Configurations** → **Indicators** → **Classification & Mapping**.
2. Do one of the following:
   1. To create a new mapper, select + New → **Indicator Mapper (incoming)**.
   2.  To edit an existing mapper, select it and click **Edit**.

       If the mapper is installed from a content pack, you need to duplicate and then edit.
3. Under **Get data**, select from where you want to import the indicator data. You will map the indicator data based on this information.
   * **Pull from instance:** Select an existing integration instance to import indicator data from.
   * **Upload JSON:** Upload a formatted JSON file that includes the fields you want to map.
4. Under **Indicator Type**, start by mapping out the **Common Mapping**. This mapping includes the fields that are common to all of the indicator types and saves you time having to define these fields individually in each indicator type.
5. Click the attribute (field) to which you want to map. You can further manipulate the field using filters and transformers.
6. Repeat this process for the other indicator types for which this mapping is relevant.
7. **Save** the mapper.
8. Apply the indicator mapper to the relevant feed integration.
   1. Navigate to Settings → **Data Sources & Integrations**.
   2. Select an existing integration instance you want to apply the classifier to or create a new integration instance.
   3. In the integration instance settings under **Mapper**, select the mapper you created and click **Save**.

</details>
