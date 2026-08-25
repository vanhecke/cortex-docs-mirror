---
description: >-
  Create and manage Cortex XSIAM base image rules for scanned registry images,
  including filters, previews, and rule updates.
---

# Create a base image rule

Before creating a rule, ensure:

* container registries are onboarded and actively scanned in your environment.
* you have **View/Edit** permission for **Compute Policies** or the **Instance Administrator** role to create or manage a **Base Images Rule**.

You can create a **Base Images** rule from either **Rules & Policies** or a **Registry Image Asset Card**.

### How to create a base images rule from **Rules & Policies**:

1. Navigate to **Posture Management** → **Rules & Policies** → **Rules** → **Base Images**.
2. Select **+ Create Rule**.
3. Enter a **Name** and optional **Description** for the rule.
4. Define the filter conditions, such as:
   * **Registry URL** (for example, **https://docker.io**)
   * **Repository** name.
5.  (Optional) Refine the filter conditions by adding additional conditions, such as:

    * **Image Name**
    * **Image Tag** (for example, **latest**).

    You can use supported operators such as **Equals**, **Not Equals**, **Contains**, **Not Contains**, starts with, and ends with to specify the conditions.
6. Select **Run Preview** to view matching images.
7.  Select **Create** to add the rule.

    The rule is automatically applied to all existing and future images that match the defined criteria. After you create or modify a **Base Images** rule, it can take up to 6 hours for the system to apply the changes and update the relationships across your assets.

### Create a base image rule from a registry image asset card

1. Navigate to **Inventory** → **Assets** → **All Assets** → **Compute** → **Container Images**.
2. Filter **Asset Type** = **Registry Image**.
3. Select a registry image row to open the details pane
4. Select the More options (**⋮**) menu.
5. Choose **Add base image rule**. The **Base Image Rules** page opens with conditions pre-populated based on the selected image.
6. Modify the conditions if required.
7. Select **Run Preview** to view matching images.
8.  Select **Create** to add the rule.

    The rule is automatically applied to all existing and future images that match the defined criteria. After you create or modify a **Base Images** rule, it can take up to 6 hours for the system to apply the changes and update the relationships across your assets.

### Manage a Base Images rule

To manage a Rule, follow these steps:

1. Navigate to **Inventory** → **Assets** → **All Assets** → **Compute** → **Container Images**.
2. Find the **Base Images** from the list of rules, or use the filter to search.
3. Select the rule row to open the details pane
4.  Select the More options (**⋮**) menu.

    | Actions         | Instructions                                                             |
    | --------------- | ------------------------------------------------------------------------ |
    | **Edit**        | Modify the existing **Base Images** rule.                                |
    | **Save as new** | Create a new rule using the existing **Base Images** rule as a template. |
    | **Delete**      | Remove the **Base Images** rule.                                         |
