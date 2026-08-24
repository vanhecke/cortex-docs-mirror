---
description: >-
  Modify the Cortex XSIAM container registry scanning scope for cloud accounts
  and registries.
---

# Modify the container registry scanning scope

Using the Modify Scanning Scope option, you can define conditions to automatically exclude selected scopes from scanning. These conditions can be based on the registry, repository, or tag. After you set the scope, the exclusion conditions are automatically applied to newly discovered images in the account.

To modify the scanning scope, do the following:

1. Navigate to **Settings** → **Data Sources**.
2. In the **Cloud Provider** section, locate the provider where your assets are stored and click **View Details**.
3. On the **Cloud Instances** page, click the instance name for which you want to modify the scope.
4. Under the **Accounts** section, select the account, right-click, and choose **Edit**.
5. Under the **Registry Scanning Scope**, enable **Modify Scanning Scope**.
6. From the list of images, select the image you want to modify.
7.  Alternatively, you can also filter for a specific image by clicking the **Filter** icon and selecting **Registry**, **Repository** ,or **Tags** option and then adding the desired value to refine your search.

    The search results are applied automatically, even if you do not select **Save**.
8. Click **Save** to confirm your modifications.

This ensures that the specified scanning scope is customized based on your needs.
