---
description: >-
  Manage Cortex XSIAM system and custom issue layouts to control Investigate
  panel fields and issue information display.
---

# Issue layouts

Manage Cortex XSIAM issue layouts to control the information displayed during issue investigation. Cortex XSIAM includes default layouts. Add layouts through content packs, duplicate system layouts, or create custom layouts. Issue layout rules apply layouts to incoming issues.

### View issue layouts in the Investigate panel

Issue layouts control information displayed in the **Investigate** panel. To view the applied layout, click **Layout Info** ![layout-info-button.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-92320ae7f1f55c4e42fa0642cd4e26e595fb9aa0%2Fc7c43472effd8964d3a4c434540e76ba09332f7a1ed01c892bf89d3f7fac96d4.png?alt=media) in the upper-right corner. Empty layout fields are hidden by default. Select **Show empty fields** to display them.

### Customize system and content pack issue layouts

Default and content pack issue layouts are locked. You cannot delete, edit, or export them. To view a system layout, right-click its row and select **View**.

To edit a system layout, detach or duplicate it from the issue layout table. A detached layout does not receive content updates until you reattach it. To reattach a system layout, right-click its row and select **Attach**. Reattaching can overwrite changes. Detached layouts can be edited or duplicated, but not deleted or exported. Duplicated layouts can be edited, deleted, or exported like custom issue layouts.

### Edit issue fields in a layout

Users with editing permissions can edit most issue fields inline. Click the check mark to save a change. Some system fields, such as **Source Instance**, cannot be edited.

### Manage custom issue layouts

To manage a custom issue layout, go to **Settings** → **Configurations** → **Object Setup** → **Issues** → **Layouts**. Right-click the layout in the table, then select **Edit**, **Duplicate**, **Delete**, or **Export**.
