---
description: Configure scanning settings for supported services in Cortex XSIAM.
---

# How to configure the scanning settings for supported services

{% hint style="info" %}
### Notice

This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

1. In the lower left area, click **Settings** → **Data Sources & Integrations**.
2. On the **Data Sources & Integrations** page, click a cloud service provider or other data source and then click the **View Details** link.
3. On the **Cloud Instances** screen, click an instance name link. A screen displaying the instance name opens.
4. At the bottom of the screen, under **Accounts** (AWS), **Subscriptions** (Azure), or **Projects** (GCP), right-click an item in the list and then in the context menu, select **Edit**.
5. In the screen that opens, under **Data assets classification options**, you can do the following:
   * Select or deselect managed services, which are native cloud services that are managed directly by your cloud provider, such as AWS, Azure, or GCP.
   * Select or deselect self-managed assets, which are databases that you run on your cloud virtual machines.
   *   Configure a cadence indicating how often a scan should be performed.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>If you do not select a scanning cadence, the default setting is applied. For more information, contact your <a href="https://support.paloaltonetworks.com/Support/Index">Customer Support team</a>.</p></div>
6.  Click **Save**.

    For more information about supported assets in Cortex Cloud Data Security, see [Supported assets in Cortex Data Security](https://app.gitbook.com/s/HfNuZNmWlqy9Bl7fETmL/data-security/supported-assets-in-cortex-data-security).
