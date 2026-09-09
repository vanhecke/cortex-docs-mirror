---
description: >-
  Discover how Cortex XSIAM detects security risks across your infrastructure,
  workloads, and container images, and how policies automate the response.
---

# Rules and Policies

### Overview

Cortex XSIAM uses rules and policies to detect security risks and manage responses across your cloud environment.

* **Rules**: Define what to check. Each rule contains the detection logic for a single condition (such as a misconfiguration, vulnerability, exposed secret, or compliance gap) and produces a finding when triggered.
* **Policies**: Define how, where, and when rules apply. A policy binds rules to a target scope (such as accounts, asset groups, namespaces, or labels) and controls severity, grace periods, and response actions.

Rules identify problems, while policies determine the response. Findings that violate an active policy become actionable issues and alerts, which feed into your overall compliance posture.

### How Rules and Policies work together

1. **Detect**: Cortex XSIAM evaluates rules against your cloud assets, workloads, and images to generate findings.
2. **Evaluate**: Findings are matched against active policies and their assigned scopes.
3. **Respond**: Findings that violate a policy (after any applicable grace periods) trigger alerts, create issues, or initiate blocking actions.
4. **Report**: Results aggregate into your overall compliance posture and reports.

### Types of Rules and Policies

Cortex XSIAM includes both built-in (out-of-the-box) and custom rules and policies.

| **Type**       | **Focus Area**                                                                            | **Key Capabilities & Frameworks**                                                                                                                                                                                                                                                                        |
| -------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cloud Security | Multi-cloud infrastructure posture (AWS, Azure, GCP, OCI)                                 | Covers CSPM, DSPM, CIEM, AISPM, and CNS. Findings map to CIS, NIST, PCI-DSS, SOC 2, and HIPAA frameworks. See [_Cloud security rules and policies_](rules-and-policies/cloud-security-rules-and-policies).                                                                                               |
| Cloud Workload | Compute workloads (VMs, Kubernetes clusters, hosts, container images, running containers) | Detects CVEs, malware, hard-coded secrets, and CIS benchmark violations. Policies let you set severity, grace periods, and enforcement actions (such as alerting or blocking noncompliant deployments). See [_Cloud workload policies and rules_](rules-and-policies/cloud-workload-policies-and-rules). |
| Base Image     | Container base ("golden") images and image inheritance                                    | Identifies base images by repository, digest, name, or tag. Attributes vulnerabilities to specific layers to separate platform or DevOps issues from application-layer issues, and detects drift in running containers. See [_Base image rules_](rules-and-policies/base-images-rule).                   |



