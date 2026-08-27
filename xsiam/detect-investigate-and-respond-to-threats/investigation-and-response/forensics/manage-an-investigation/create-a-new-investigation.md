---
description: >-
  Create forensic investigations to organize collections, evidence, alerts, and
  user access with Cortex XSIAM.
---

# Create a new investigation

Create a forensics investigation that includes all the relevant forensics data. This includes adding collections (hunts and triages), exporting the data collections, managing alerts and evaluating key assets & artifacts.

1. Select **Investigation & Response** → **Forensics**.
2. Click **New Investigation**.
3. In the **Create New Investigation** wizard, enter a name and description (optional) for the investigation.
4.  In the **Permissions** table, select the users to whom you want to grant access to the investigation data.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>To set up user permissions, you must have Scope-Based Access Control (SBAC) enabled.</p></div>

    Refer to [User permissions](user-permissions) for detailed information on permissions.
5. Click **Save** to save the investigation in the **Forensic Investigations** table or click **Save & Start A Collection** to start the process of adding collections.
6. In the **New Collection** widget, select [**Triage**](../data-collection/triage) or [**Hunt**](../data-collection/hunting).
7. The investigation is saved to the **Forensic Investigations** table.
8. Click **UTC Timezone** to configure the timezone and timestamp format. Refer to [Configure server settings](../../../../onboard-cortex-xsiam/post-deployment/configure-server-settings) for information on setting up your timezone.
