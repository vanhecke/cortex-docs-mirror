# Create a sync profile

Sync profiles provide a blueprint for how information is exchanged between Cortex XSIAM issues and external applications, by defining field mapping. This ensures that relevant data, such as **Status** or **Description**, is accurately transferred and maintains consistency, even if the systems use different terminology.

When you link an issue with an external application (such as Jira), or set up an automation, you can select the sync profile you want to use. Cortex XSIAM provides default outbound and inbound sync profiles, or you can create custom sync profiles as described in the following procedure.

How to create a sync profile

1. Go to **Settings** → **Configurations** → **Object Setup** → **Issues** → **Sync Profiles**.
2. Click **New Profile**.
3. Type a profile name and description.
4. Under **Integration**, select the external application with which you want to map fields, such as Jira V3 or ServiceNow V2.
5.  Under **Sync Direction**, select **Inbound** or **Outbound**.

    If you select **Inbound**, you will define field mapping from the external application to Cortex XSIAM. If you select **Outbound**, you will define field mapping from Cortex XSIAM to the external application.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If an issue is using bi-directional syncing, you need to provide both an Inbound and an outbound sync profile.</p></div>
6. Under **Field Mapping**, select a field to map and select the corresponding field. For example, Jira: Priority, Cortex: Severity.
7.  Define one or more values for each field that you want to map.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><ul><li>Blank fields are skipped.</li><li>You must define exact values.</li><li>Custom status values are not currently supported.</li><li>Support is currently limited to a specific set of fields.</li></ul></div>
8.  Click **Save**.

    In this example, the sync profile specifies Inbound mapping from Jira v3 fields to Cortex fields.

    ![Sync\_profile\_example.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-56ef61bdbc2dfd2c2bda4ba0285e62008f1e4501%2F053eb012a06adcbc9feebb449ef1949a784deff31c746a3e69ca4c197f36cb15.png?alt=media)
