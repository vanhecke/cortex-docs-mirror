---
description: Learn which health checks to perform after deployment.
---

# Perform health checks

As part of the onboarding process, it is recommended to perform the following health checks:

* **Update prevention policies:** Update policies and profiles and ensure that all action modes are set to Block. For more information, see Set up endpoint profiles and exception rules in the Cortex XSIAM Administrator Guide.
* **Monitor operational status:** Verify that Cortex XDR agents are protecting endpoints according to predefined security policies and profiles. For more information, see [Monitor agent operational status in Cortex XSIAM](perform-health-checks/monitor-agent-operational-status-in-cortex-xsiam).
* **Test sample malware:** Use a malware PE, MacOSX, or APK test file, to test end-to-end WildFire sample processing. For more information, see [Get a Malware Test File](https://docs.paloaltonetworks.com/wildfire/u-v/wildfire-api/get-wildfire-information-through-the-wildfire-api/get-a-malware-test-file-wildfire-api).
* **Validate detectors for issues and cases:** Check issues and their associated sources. Validate that all the configurations on the policy level and on the agent deployment level meet the requirements to generate alerts and cases on Cortex XSIAM. For example, check the following:
  * Cortex XDR agent generates WildFire malware issues.
  * NFGW issues are listed by PAN NGFW.
* **Validate log ingestion from external integrations:** Verify what datasets are being created. The **Dataset Management** page enables you to manage your datasets and understand your overall data storage duration for different retention periods and datasets based on your Hot and Cold Storage licenses, and retention add-ons to extend your storage. For more information, see [Data storage lifecycle](../../learn-about-cortex-xsiam/cortex-xsiam-product-licenses/data-storage-lifecycle).
