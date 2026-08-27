---
description: Manage the Harbor registry connector in Cortex XSIAM.
---

# Manage a Harbor connector

After successfully adding a connector, you can modify the connector settings and configure the scanning scope to control which images are scanned in the connected registry.

To manage the connector, follow these steps:

1. Navigate to **Settings → Data Sources & Integrations**.
2. Find the **Harbor** data source from the list of data sources, or use the filter to search.
3.  Select the **Harbor** row. A pane opens with a list of integration instances and their details.

    You can create a new instance by selecting **Add Instance** and following the [onboarding wizard]() to define the settings.
4.  Right click an instance to perform actions on it as follows:

    <table><thead><tr><th width="223.14453125">Action</th><th>Instructions</th></tr></thead><tbody><tr><td><strong>Edit</strong></td><td><p>Edit the Harbor instance.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h4>Note</h4><ul><li>If you selected <strong>Scan with Broker VM</strong> mode, you can't change to a different scan mode (such as <strong>Cloud Discovery</strong> or <strong>Scan with Outpost</strong>) when you edit the instance.</li><li>When editing an instance configured for <strong>Scan with Broker VM,</strong> you must re-enter your authentication credentials, including <strong>Username</strong>, <strong>Password</strong>, and <strong>CA certificate</strong>.</li></ul></div></td></tr><tr><td><strong>Exclude/Include images</strong></td><td>Define conditions to automatically exclude or include specific images while scanning. Conditions can be based on <strong>Repository</strong> or <strong>Tags</strong>. These conditions apply automatically to newly discovered images in the account.</td></tr><tr><td><strong>Delete</strong></td><td>Removes the connector.</td></tr><tr><td><strong>Disable</strong></td><td>Stops image scanning for the connector without deleting it.</td></tr></tbody></table>
