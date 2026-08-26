---
description: >-
  Investigate internet-exposed cloud assets in Cortex XSIAM using Issues and
  Graph Search to prioritize and remediate risk.
---

# Investigate an internet exposure

You can investigate assets exposed to the internet by reviewing issues detected by Cloud Network Analyzer or by using Graph Search.

### **Investigate internet exposure issues**

Review internet exposure issues to learn which assets are exposed to the internet. You can find internet exposure issues under **Cases & Issues**.

1. Go to **Cases & Issues**.
2. Select the **Detection Method** filter and then select the **Cloud Network Analyzer** as the **Detecting Engine**.
3. Select a specific issue to investigate. You can review:
   * Affected asset
   * Policy that triggered the exposure
   * Exposure details (Public IP, FQDN, protocol, port, and HTTPs response code)
   * Exposure path
4.  From an issue, you can navigate to a specific affected asset and investigate further by clicking on the **Network** tab. The Network tab provides in-depth visibility over specific network details and internal network reachability:

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>NOTE:</strong></p><p>The <strong>Network</strong> tab is currently only available for virtual machines.</p></div>

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>NOTE:</strong></p><p>The <strong>Network</strong> tab is only displayed when you have access to the main asset and associated ones, such as security groups, VPCs and subnets. For more information on Scope-Based Access Control (SBAC) for configuring granular scoping, see Manage user scope.</p></div>

    * **Networking Details:** Access details such as where the VM is deployed, connected subnets, and associated network security controls. Review a visual representation of the asset and all the private IPs connected to it.
    * **Networking Security Rules:** An interface to investigate the network rules associated with the asset.

### **Investigate internet-exposed assets using Graph Search**

You can use What is Graph Search? to search for and investigate internet-exposed assets.

1. Go to **Investigation and Response → Search → Query Builder → Graph Search**.
2. Define a query that finds selected assets where Internet Exposed = True:
   1. Select one or more specific asset types that are supported by CNA exposure detection, such as a **Virtual Machine** or a **Kubernetes Workload**.
   2. Add a condition **WHERE Internet Exposed = True**.
3. Click **Search**.
4. Click on an object and then click on **View Details** to view details of the asset.
5.  Investigate further by clicking on the **Network** tab. The **Network** tab provides in-depth visibility over specific network details and internal network reachability:

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>The <strong>Network</strong> tab is currently only available for virtual machines.</p><p>The Network tab is only displayed when you have access to the main asset and associated ones, such as security groups, VPCs and subnets. For more information on Scope-Based Access Control (SBAC) for configuring granular scoping, see Manage user scope.</p></div>

    * **Networking Details:** Access details such as where the VM is deployed, connected subnets, and associated network security controls. Review a visual representation of the asset and all the private IPs connected to it.
    * **Networking Security Rules:** An interface to investigate the network rules associated with the asset.
