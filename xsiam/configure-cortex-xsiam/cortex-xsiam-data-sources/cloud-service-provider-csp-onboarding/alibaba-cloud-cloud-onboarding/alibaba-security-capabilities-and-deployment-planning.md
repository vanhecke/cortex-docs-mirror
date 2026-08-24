---
description: Plan Alibaba Cloud security capabilities for Cortex XSIAM onboarding.
---

# Alibaba security capabilities and deployment planning

## **Security capabilities and deployment planning**

Plan your deployment by reviewing the security capabilities available for Alibaba Cloud. The onboarding process deploys the capabilities using a single Terraform connector template. Alibaba Cloud onboarding currently supports two capabilities: Discovery and Permissions. No additional capabilities (such as agentless disk scanning, data security, audit logs, registry scanning, serverless scanning, or automation) are currently supported.

### **Core capabilities (Discovery and Permissions)**

The Discovery and Permissions capabilities are mandatory and are deployed automatically when you onboard an Alibaba Cloud account to Cortex XSIAM. Discovery inventories cloud resources across supported services, while Permissions analyzes IAM configurations and monitors access policies.

| Module      | Identity created              | Resources created                                         | Purpose                                                                                                                 | Regional scope                    |
| ----------- | ----------------------------- | --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| Discovery   | CortexPlatformRole (RAM role) | RAM Role, Custom Policy, Policy Attachment, OIDC Provider | Read-only discovery and inventory of Alibaba Cloud resources across ECS, OSS, VPC, RDS, SLB, CEN, ActionTrail, and NAS. | All supported internal regions.   |
| Permissions | CortexPlatformRole (RAM role) | RAM Role, Custom Policy, Policy Attachment, OIDC Provider | IAM permission analysis and monitoring across RAM users, roles, groups, and policies.                                   | Global (RAM is a global service). |

### **Read-only permissions by service**

The Terraform template provisions a custom RAM policy with 46 read-only permissions grouped by Alibaba Cloud service:

<table><thead><tr><th width="146.5703125">Service</th><th>Permissions</th></tr></thead><tbody><tr><td>ECS</td><td>DescribeInstances, DescribeDisks, DescribeInstanceRamRole, DescribeSecurityGroups, DescribeSecurityGroupAttribute</td></tr><tr><td>OSS</td><td>ListBuckets, GetBucketInfo, GetBucketLogging, GetBucketVersioning</td></tr><tr><td>RAM</td><td>ListUsers, ListRoles, ListGroups, ListPolicies, GetPolicy, GetPolicyVersion, ListPoliciesForUser, ListPoliciesForRole, ListPoliciesForGroup, GetLoginProfile, GetUserMFAInfo, ListAccessKeys, GetPasswordPolicy</td></tr><tr><td>RDS</td><td>DescribeDBInstances, DescribeDBInstanceIPArrayList, DescribeDBInstanceSSL, DescribeDBInstanceEncryptionKey, DescribeDBInstanceTDE, DescribeDBInstanceAttribute</td></tr><tr><td>VPC</td><td>DescribeVpcs, DescribeFlowLogs, DescribeVpnConnections, DescribeVpnConnection, DescribeSslVpnServers</td></tr><tr><td>SLB</td><td>DescribeLoadBalancers, DescribeLoadBalancerAttribute, DescribeVServerGroups, DescribeMasterSlaveServerGroups, DescribeCACertificates, ListTLSCipherPolicies, DescribeLoadBalancerHTTPSListenerAttribute</td></tr><tr><td>ActionTrail</td><td>DescribeTrails, GetTrailStatus</td></tr><tr><td>CEN</td><td>DescribeCens, DescribeCenInterRegionBandwidthLimits</td></tr><tr><td>NAS</td><td>DescribeFileSystems</td></tr></tbody></table>
