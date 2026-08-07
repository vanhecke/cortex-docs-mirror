# Outbound exposure detection

CNA supports outbound internet exposure detection. If CNA detects a workload that based on their security configurations has unrestricted internet access, CNA generates a finding.

This helps you determine which assets have potentially unrestricted access to the internet, taking into account the effect of cloud native security controls, network firewalls and NAT gateways. It allows you to:

* Visualize the complete network path of an asset from source to destination.
* Periodically re-validate the status of an exposed asset.
* Find which security group or firewall rule is causing the exposure.

**Outbound exposure rules**

Outbound exposure rules do not have out of the box rules, but you can create custom ones. See [Create a Network Exposure Rule](../cloud-security-rules-and-policies/create-and-manage-cloud-security-rules/create-a-network-exposure-rule).

**Supported asset types**

CNA can detect outbound internet exposure in the following cloud services and asset types:

| **Provider/ Service**        | **AWS**    | **Azure** | **GCP** |
| ---------------------------- | ---------- | --------- | ------- |
| **Managed virtual machines** | Amazon EC2 | –         | –       |
