---
description: >-
  Configure trusted public IP ranges excluded from CNA internet exposure
  evaluations.
---

# Configure trusted IPs

You can define specific public IP ranges (CIDR blocks) that belong to your company, partners, or trusted services. By designating these networks as "trusted," the system will exclude them from Cloud Network Analyzer (CNA) internet exposure evaluations. This prevents assets from being flagged as "internet exposed" when they are only accessible to known and trusted external networks, reducing unnecessary security findings and noise.

The following restrictions apply when defining trusted networks:

* You must provide a valid public IPv4 address.
* Only public CIDR blocks are supported. CIDR blocks must not be within the RFC 1918 private network range.

## **Add a trusted network**

You can define a trusted network by specifying and describing an external IPv4 address range or by uploading a CSV file with IP address ranges.

1. Navigate to **Inventory → Network Configuration → Trusted Networks**.
2. Click the **+Add trusted networks** and choose one of the following methods:
   1. **Create New**: Specify Name, Description (Optional) and single valid public IPv4 CIDR range.
   2. **Upload from File:** You can bulk-upload ranges using a CSV file. The file must follow the format presented in the example below. You can also download the example file from the UI.
3. Click **Update** to save the trusted network.

Once it is saved, the specified network is automatically considered by CNA as a trusted network.

### **CSV file example**

The CSV file should look similar to the following, with one external network per line:

```
Name,CIDR Range,Description 
My Network 1,200.0.0.0/8,Example description 
Another Network 2,200.0.0.0/24,Another example
```

## **Edit a trusted network**

To modify an existing configuration, navigate to **Inventory → Network Configuration → Trusted Networks**, right-click the configuration, and then select **Edit**.

**Delete a trusted network**

To delete a configuration, navigate to **Inventory → Network Configuration → Trusted Networks**, right-click the existing entry, and select **Delete**.
