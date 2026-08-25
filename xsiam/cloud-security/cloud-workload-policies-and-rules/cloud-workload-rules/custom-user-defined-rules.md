---
description: >-
  Create Cortex XSIAM custom cloud workload rules for organization-specific
  security, compliance, and misconfiguration checks.
---

# Custom (user-defined) rules

Custom Rules or Custom Detection Rules allow you to define and implement tailored security and compliance checks within cloud workloads. These rules enable organizations to detect specific conditions, vulnerabilities, or misconfigurations that might not be covered by built-in system rules.

A custom rule consists of the following components:

* **Scanner:** Defines the mechanism by which the rule inspects the cloud assets. You need to select the scanner type that will implement the rule. Every time the selected scanner runs, all the rules associated with that scanner are also executed. The available scanner types are:
  * **Agentless Disk Scan:** Rules that use Agentless Disk Scanner to inspect the container images on which the Agentless scanner runs. You can specify different rules for containers running different OSes. For example, you can create a rule that checks for incorrect or malicious entries in the etc\hosts file on Windows images.
  * **Kubernetes Connector:** Rules that use the Kubernetes Connector scanner to inspect Kubernetes environment variables and resources such as Namespaces, ReplicaSets, Deployments and more.
  * **XDR Agent:** Rules that use XDR Agent Scanner to perform custom compliance checks by executing user-defined Python scripts, offering a tailored approach to compliance validation.
* **Rule (Condition):** Defines the detection criteria. This is specified as Rego or Python statements that evaluate assets, findings, and their associated attributes to identify security violations based on the selected scanner.
* **Severity:** The selected value is included in issues that are created as a result of rule violation.
* **Compliance Controls:** Associates the custom rule with a custom compliance control. If the rule detects the security violation, it will invoke the corresponding compliance control, thereby including the violation in relevant compliance reports.
