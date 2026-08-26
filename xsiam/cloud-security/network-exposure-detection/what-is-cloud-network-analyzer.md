---
description: >-
  Learn how Cloud Network Analyzer in Cortex XSIAM identifies internet,
  outbound, and lateral exposure risks across cloud accounts.
---

# What is Cloud Network Analyzer?

Cloud Network Analyzer (CNA) in Cortex XSIAM determines which assets—such as virtual machines, databases, containers, and serverless functions—are exposed to the internet, have unrestricted access to the internet, or can laterally move within a cloud account.

CNA creates an internal network topology to map the path between the internet and the asset. This map provides insights about existing network security controls, including security groups and internet gateways.

CNA helps you identify the following:

* Workloads exposed to access from the internet
* Workloads that have unrestricted outbound access to the internet
* Overly permissive security groups attached to sensitive workloads
* Production applications connected to testing or staging environments between cloud accounts or VPCs
* Object storage buckets with sensitive data exposed through network connectivity to external cloud accounts or networks
* Kubernetes services exposed to access from the internet, their underlying endpoints, and associated deployments

### Detection capabilities: inbound, outbound, east-west

CNA detects which assets are exposed to the internet, have unrestricted access to the internet, or can laterally move within a cloud account. CNA supports three types of internet exposure detection:

* **Inbound:** Data or requests entering your network from external sources
* **Outbound:** Data or requests leaving your network to external destinations
* **East-west:** Data or requests moving laterally within your network

Inbound exposure detection is referred to as “Internet exposure detection” in this documentation.
