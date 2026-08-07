---
description: >-
  After you have completed the Alibaba Cloud onboarding wizard and you have
  deployed the authentication template in Alibaba Cloud, verify that the
  deployment succeeded.
---

# Alibaba Cloud post-deployment verification

After you have deployed the authentication template in Alibaba Cloud, verify that it was successfully deployed. InCortex Cloud, select **Data Sources & Integrations → Cloud Accounts**. Verify the following:

* The original cloud instance remains in "Pending" state. For more details on pending instances, see Understand pending instances.
* A new cloud instance appears in the cloud accounts list (separate from the pending instance).
* The new cloud instance shows status "Connected".
* The discovery scan starts automatically for every discovered account.
* Assets appear in the **Asset Inventory** as discovery progresses.

### **Troubleshooting Alibaba Cloud onboarding**

If no new cloud instance appears, ensure you [manually connect the cloud instance](../manually-connect-a-cloud-instance) to create the instance from the pending cloud instance.
