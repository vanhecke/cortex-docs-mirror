---
description: Map integration fields to issue types in Cortex XSIAM.
---

# Map fields to issue types

Mappers enable you to map information from incoming events to the issue fields that you have in your system. You can map to system issue fields or custom issue fields.

Mapping event attributes or issue fields takes place in two stages. First you map all of the fields that are common to all issues in the default mapping. Second, you map the additional fields that are specific for each issue indicator type, or overwrite the mapping that you used in the default mapping.

{% hint style="info" %}
### Note

In the **Classification & Mapping** page, the mapping does not indicate for which issue types they are configured. Therefore, when creating a mapper, it is best practice to add to the mapper name, the issue types the mapper is for. For example, Mail Listener - Phishing.
{% endhint %}

{% hint style="info" %}
### Note

When mapping a list, we recommend you map to a multi select field. Short text fields do not support lists. If you do need to map a list to a short text field, add a transformer in the relevant playbook task, to split the data back into a list.
{% endhint %}

You can use this procedure for creating a classifier or duplicating an existing mapper for issue types.

1. Navigate to Settings → Configurations → **Object Setup** → Issues → **Classification & Mapping**.
2. Click **New** and select **Issue Mapper (incoming)**. The Issue Mapper maps all of the fields you are pulling from the integrations to the issue fields in your layouts.
3. Under **Get data**, select from where you want to pull the information based on where you want to map the issue types.
   * Pull from instance - select an existing integration instance.
   * Select schema - when supported by the integration, this pulls all of the fields for the integration from the database. This enables you to see all of the fields for each given event type that the integration supports.
   * Upload JSON - upload a formatted JSON file which includes the field you want to map.
4. Under **Issue Type**, start by mapping out the **Common Mapping**. This mapping includes the fields that are common to all of the issue types and will save time having to define these fields individually in each issue type.
5.  Click the event attribute to which you want to map. You can further manipulate the field using filters and transformers.

    You can click **Auto Map** to automatically map fields with common or similar names to fields in Cortex XSIAM . For example, Severity to Importance or Description to Description.
6. Repeat this process for the other issue types for which this mapping is relevant.
7. Click **Save**.
8. Go to Settings → **Data Sources & Integrations**.
   1. Select the integration instance to which you want to apply the mapper.
   2. In the integration settings, under **Mapper (incoming)** select the mapper you created and click **Save**.
