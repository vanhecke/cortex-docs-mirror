# Find the base image for an asset

Container image assets include **Base Image** details that identify the foundational registry image they are derived from. If an asset is a base image, a **Base Image** property is displayed in the asset side panel.

When a Base Images Rule is created, a base image tag is assigned to matching container image assets. You can use this tag to create an **Asset Group** ( **Inventory** → **Assets** → **Groups**) by filtering on the **Image Is Base Image**. This allows you to group all base images and use the asset group for policies and issue management.

### How to find the base image for an asset

1. Navigate to **Inventory** → **Assets** → **All Assets** → **Compute** → **Container Images**.
2. Open a container image asset (**Registry Image** or **Runtime Image**).
3. In the **Overview** tab, under the **Properties** section, locate **Base Image** details to view the linked foundational registry image.
4. View the **Relationships** section to explore upstream and downstream image lineage.
