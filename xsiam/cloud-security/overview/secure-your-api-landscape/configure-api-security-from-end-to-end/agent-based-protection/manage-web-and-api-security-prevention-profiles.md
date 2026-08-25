---
description: >-
  Manage Cortex XSIAM Web and API Security prevention profiles, including policy
  usage, editing, exporting, and deletion.
---

# Manage Web and API Security prevention profiles

After you create and customize your Web and API Security prevention profiles, you can manage them from the **Prevention Profiles** page as needed.

<details>

<summary>View the prevention policy rules that use a specific prevention profile</summary>

Before you modify or delete a profile, you can check which policy rules, if any, use the profile.

*   From **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, right-click the profile and select **View policy Rules**.

    Cortex XSIAM opens the **Prevention Policy Rules** page on a new tab. This page is filtered, and only displays the rules that use the profile that you selected.

</details>

<details>

<summary>Edit, export, duplicate, or delete a prevention profile</summary>

Edit a profile:

1. From **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, right-click the profile and select **Edit**.
2. Make your changes, and then click **Save**.

Export a profile:

1. From **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, right-click the profile and select **Export Profile**.
2. Click **Export**. The profile is downloaded to your computer.

Duplicate a profile:

1. From **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, right-click the prevention profile and select **Save as New**. A new profile is displayed, containing the values from the profile that you selected.
2. Edit the profile name and description, edit any values that you want to change, and then click **Create**.
3. Populate a new prevention policy rule with your new profile.

Delete a profile:

1. If necessary, delete or detach any policy rules that use the profile before attempting to delete it.
2. From **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, locate the profile that you want to remove. The profile's **Usage Count** cell must have a 0 (zero) value.
3. Right-click the prevention profile and select **Delete**.
4. To confirm the deletion, click **Yes**.

</details>

<details>

<summary>Populate a new prevention policy rule with a prevention profile</summary>

1.  From **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**, right-click the profile and select **Create a new policy rule using this profile**.

    Cortex XSIAM automatically populates the **Platform** selection based on your profile configuration, and assigns the profile based on the profile type.
2. For **Policy Name**, enter a meaningful name, and optionally, add a description for the policy rule.
3. Assign any additional profiles that you want to apply to your policy rule, and click **Next**.
4. Select the target workloads for the policy rule, or use the filters to define criteria for the policy rule to apply, and then click **Next**.
5. Review the policy rule summary, and then click **Done**.

</details>

#### **View information about your Web and API Security prevention profiles**

The following table displays the fields that are available on the **Prevention Profiles** page, in alphabetical order. The table includes both default fields and additional fields that are available in the column manager. To view this page, go to **Inventory** → **Endpoints** → **Policy Management** → **Prevention** → **Profiles**.

| Field              | Description                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------- |
| Associated Targets | The endpoints or endpoint groups to which the profile is assigned                                                     |
| Created By         | The administrator who created the prevention profile                                                                  |
| Created Time       | The date and time at which the prevention profile was created                                                         |
| Description        | An optional description entered by an administrator to describe the prevention profile                                |
| Modification Time  | The date and time at which the prevention profile was modified                                                        |
| Modified By        | The administrator who modified the prevention profile                                                                 |
| Name               | The prevention profile name                                                                                           |
| Profile ID         | The ID assigned to to the profile by Cortex XSIAM                                                                     |
| Summary            | Summary of prevention profile configuration                                                                           |
| Type               | The prevention profile type                                                                                           |
| Usage Count        | The number of policy rules that use the profile. If you want to delete a profile, ensure that this cell displays "0". |
