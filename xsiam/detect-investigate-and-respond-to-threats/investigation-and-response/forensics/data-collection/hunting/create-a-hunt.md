---
description: >-
  Create Cortex XSIAM hunt collections for scheduled or one-time endpoint
  artifact searches.
---

# Create a hunt

Select hunt collections when you want to search for a specific activity across a large number of hosts. Hunt Collections gather more details about where something occurred. For example, use a hunt to find which endpoints executed a piece of malware, which users accessed a particular file, or which endpoints a specific user authenticated to.

When adding a new hunt collection in Cortex XSIAM, you can select from various artifact types for Windows, macOS and Linux.

1. In the **New Hunt Collection** wizard, in the **Hunt Collection Name**, enter a name that will be easy to find in the collections table.
2. Select the **Platform**, Windows, macOS or Linux.
3. Select one of the time range options:
   * **One Time Collection**: Run the hunt collection only once.
   * **Repeat Collection Every**: Run the hunt collection every x hours set.
   * **Schedule**: Range of days during the week and time frame.
4. In **Description**, enter information that is relevant to the collection you are creating.
5. In **Maximum Concurrent Endpoints**, enter the maximum number of endpoints that will run the searches at the same time within the time range specified. The default is 200 endpoints.
6. On the **Configuration** page, refer to [Configure Collection](../configure-collection) for information about each artifact.

{% hint style="info" %}
You can save hunts in an incomplete state and edit them later. After a hunt has run, you cannot edit it. Instead, you can duplicate the hunt with the same configuration.
{% endhint %}
