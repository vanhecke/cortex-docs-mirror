---
description: Review XDR Collector datasets in Cortex XSIAM.
---

# XDR Collector datasets

After Cortex XSIAM begins receiving data from your XDR Collectors configuration, the app automatically creates an XQL dataset.

After Cortex XSIAM begins receiving data from your XDR Collectors configuration that are dedicated for on-premises data collection on Windows and Linux machines.

* For Filebeat, the app automatically creates an Cortex Query Language (XQL) dataset of event logs using the vendor name and the product name specified in the configuration file section of the Filebeat profile. The dataset name follows the format `<vendor>_<product>_raw`. If not specified, Cortex XSIAM automatically creates a new default dataset in the format `<module>_<module>_raw` or `<input>_<input>_raw`. For example, if you are using the NGINX module, the dataset is called `nginx_nginx_raw`.
* For Winlogbeat, the app automatically creates an XQL dataset of event logs using the vendor name and the product name specified in the configuration file section of the Winlogbeat profile. The dataset name follows the format `<vendor>_<product>_raw`. If not specified, Cortex XSIAM automatically creates a new default dataset, `microsoft_windows_raw`, for event log collection. Winlogbeat data is also normalized to `xdr_data` (and thus the `xdr_event_log` preset).

After Cortex XSIAM creates the dataset, you can search for your XDR Collector data using XQL Search.
