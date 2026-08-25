---
description: >-
  Create Cortex XSIAM sync profiles to map issue fields and synchronize data
  with Jira, ServiceNow, and other external applications.
---

# Create a sync profile

Create Cortex XSIAM sync profiles to map issue fields and synchronize issue data with external applications. Field mapping transfers values such as **Status** and **Description** accurately, even when systems use different terminology.

When you link an issue to an external application, such as Jira or ServiceNow, or configure an automation, select the required sync profile. Cortex XSIAM provides default inbound and outbound sync profiles. You can also create custom profiles.

### Create a Cortex XSIAM issue sync profile

1. Go to **Settings** → **Configurations** → **Object Setup** → **Issues** → **Sync Profiles**.
2. Click **New Profile**.
3. Type a profile name and description.
4. Under **Integration**, select the external application for field mapping, such as Jira V3 or ServiceNow V2.
5.  Under **Sync Direction**, select **Inbound** or **Outbound**.

    **Inbound** maps fields from the external application to Cortex XSIAM. **Outbound** maps fields from Cortex XSIAM to the external application.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you use bi-directional syncing, you need to provide both an Inbound and an Outbound sync profile.</p></div>
6. Under **Field Mapping**, select a field to map and select the corresponding field. For example, Jira: Priority, Cortex: Severity.
7.  Define one or more values for each field that you want to map.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>Blank fields are skipped.</li><li>You must define exact values.</li><li>Custom status values are not currently supported.</li><li>Support is currently limited to a specific set of fields.</li></ul></div>
8.  Click **Save**.

    In this example, the sync profile specifies Inbound mapping from Jira v3 fields to Cortex fields.

    ![Sync\_profile\_example.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-56ef61bdbc2dfd2c2bda4ba0285e62008f1e4501%2F053eb012a06adcbc9feebb449ef1949a784deff31c746a3e69ca4c197f36cb15.png?alt=media)
