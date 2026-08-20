---
description: >-
  Explore the Cortex XSIAM architecture, including SIEM, XDR, SOAR, cloud
  security, XDL data ingestion, and Broker VM.
---

# Cortex XSIAM architecture

### Cortex XSIAM architecture overview

Cortex XSIAM unifies endpoint, network, cloud, identity, and third-party security data. Its architecture combines AI-driven detection, investigation, and response with centralized data ingestion, normalization, and automation.

![Cortex XSIAM architecture showing core security capabilities and Cortex Extended Data Lake](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-20782514fe7bf7ea892a4605517c87259ca2869b%2F60909af9f63a0506b23aa65a0d22ff5eb5596b010af64e063b988e22be57d051.png?alt=media)

### Core Cortex XSIAM capabilities

* Cortex XSIAM includes:
  * **SIEM** (security information and event management)
  * **EDR/XDR** (endpoint and extended detection and response)
  * **CDR** (cloud detection and response), including Cloud Posture and Cloud Runtime Security
  * **NDR** (network detection and response)
  * **SOAR** (security orchestration, automation, and response)

### Cortex Extended Data Lake (XDL)

*   Cortex Extended Data Lake (XDL) provides unified data normalization, AI, and automation. It centralizes security telemetry as a single, intelligent source of truth, including:

    | Feature                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
    | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Endpoint                      | <p>Cortex XDR agents forward all data directly to Cortex XDL. This data is accessible for query and investigation within Cortex XSIAM.</p><p>When a Cortex XDR agent detects an unknown sample (an attempt to run a macro, DLL, or executable file), Cortex XSIAM can automatically forward the sample for WildFire analysis. WildFire Cloud Service identifies previously unknown malware and generates signatures that Palo Alto Networks firewalls and Cortex XSIAM can use to detect and block that malware.</p><p>Based on the properties, behaviors, and activities the sample displays when analyzed and executed in the WildFire sandbox, WildFire determines whether the sample is benign, grayware, phishing, or malicious. WildFire then generates signatures to recognize the newly discovered malware and makes the latest signatures globally available every five minutes.</p> |
    | Network & SASE                | <p>Centralizes logs from Palo Alto Networks sources. It utilizes the Strata Logging Service to ingest and normalize network logs from Next-Generation Firewalls (NGFW) and Prisma Access.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If you plan to stream data from a Strata Logging Service instance, it must reside in the same region as your Cortex XSIAM tenant.</p></div>                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
    | Cloud, Apps & CI/CD           | Provides comprehensive visibility across your cloud infrastructure, version control systems (VCS), and delivery pipelines to detect risks, such as exposed secrets, Software Composition Analysis (SCA) vulnerabilities, and IaC misconfigurations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
    | Identity                      | <p>Consumes data from identity sources that connect to the Cloud Identity Engine, which provides the necessary Active Directory or Okta context for User/Entity Behavior Analytics (UEBA).</p><p>The Cloud Identity Engine (CIE) enables Palo Alto Networks cloud-based applications to use computer, user, and group attributes from your organization’s directories for security policies and endpoint management. This cloud-based service synchronizes attribute data from various sources, including On-prem directories like Active Directory and cloud-based directories such as Microsoft Entra ID, Okta, and Google Cloud Identity.</p><p>The Cortex XSIAM tenant and the CIE must be deployed in the same region.</p>                                                                                                                                                               |
    | Vulnerabilities and exposures | ASM performs DNS lookups and scans hosts to identify security flaws before they can be exploited. The intelligence gathered from these lookups and scans is transformed into actionable data, such as vulnerabilities and exposures.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
    | Open ecosystem (any source)   | Facilitates the ingestion of third-party security and management vendor telemetry, custom logs, and external alerts from any environment. These sources are integrated into Cortex XDL using an HTTP Log Collector or through the Broker VM, which runs specialized applets for Syslog, Database, CSV, Kafka, and FTP collection                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### Extended Cortex XSIAM capabilities

You can extend Cortex XSIAM with capabilities such as:

* ITDR (Identity Threat Detection and Response) for domain controller protection
* Threat Intelligence Platform (TIP)&#x20;
* Attack Surface Management (ASM)
* Email Advanced Security
* Exposure Management

### Cortex Agentic Assistant

Cortex Agentic Assistant uses AI agents to plan, reason, and investigate complex threats. Examples include cloud identity theft and container breaches.

### Cortex XSIAM ecosystem

This diagram shows Cortex XSIAM as a central security operations platform. It connects diverse data sources and proactive security functions.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2FQbAfFWWNgsBueFKYXxbU%2Fimage.png?alt=media&#x26;token=f3c44fd2-b0f1-4840-a860-8239e9e57350" alt="Cortex XSIAM ecosystem connecting security data sources, XDL, and proactive security functions"><figcaption><p>Cortex XSIAM ecosystem architecture.</p></figcaption></figure>

### Broker VM architecture and data collection

Broker VM is a secure on-premises gateway for Cortex XSIAM data ingestion. It centralizes collection from security devices that cannot send data directly to the cloud. It also provides a secure proxy for agents and collectors in restricted or air-gapped networks. Specialized applets collect different data types and ingest them into Cortex XDL.

<figure><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fs2fhystfiBuytnXX7Gj3%2Fbroker-vm.png?alt=media&#x26;token=0113b5f8-5763-4262-b894-577d1aa66dea" alt="Cortex XSIAM Broker VM architecture for secure on-premises data collection"><figcaption><p>Broker VM data collection architecture.</p></figcaption></figure>
