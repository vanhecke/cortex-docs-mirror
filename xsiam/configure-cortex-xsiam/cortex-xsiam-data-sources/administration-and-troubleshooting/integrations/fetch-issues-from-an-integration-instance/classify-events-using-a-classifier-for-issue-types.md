---
description: Classify integration events for issue types in Cortex XSIAM.
---

# Classify events using a classifier for issue types

When an integration fetches issues, it populates the rawJSON object in the issue object. The rawJSON object contains all of the attributes for the event. For example, source, when the event was created, the priority that was designated by the integration, etc. When classifying the event, you want to select an attribute that can determine the event type.

You can use this procedure for creating a classifier or duplicating an existing classifier.

1. Go to Settings → **Configurations** → **Object Setup** → **Issues** → **Classification & Mapping**.
2.  Click **New** and select **Issue Classifier**.

    If you want to duplicate the classifier, select the relevant classifier and then duplicate it.
3. Under **Get data**, select from where you want to pull the information based on which you will classify the issue types.
   * Pull from instance - select an existing integration instance.
   * Select schema - when supported by the integration, this will pull all the fields for the integration from the database from which you can select by which to classify the events.
   * Upload JSON - upload a formatted JSON file which includes the field by which you want to classify.
4. In the **Select Instance** field, select the instance from where you want to choose the value.
5. In the **Data fetched from** select the value by which you want to classify the events.
6.  Drag values from the **Unmapped Values** column to the relevant issue type on the right.

    You can optionally choose a default issue type for unclassified issues from **Direct unclassified events to: Select**.

    ![classifier.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-43ce71407bf3a2f8d21c5d9f85744bc8f505971f%2Fb13f2487cd6f1a3cf25caa201c9c8135b7887336f8a480e46f358218b8a09d0a.png?alt=media)
7. Click **Save**.
8. Go to **Settings** → **Data Sources & Integrations**.
   1. Select the integration to which you want to apply the classifier.
   2. In the integration settings, under **Classifier**, select the classifier you created and click **Save**.
