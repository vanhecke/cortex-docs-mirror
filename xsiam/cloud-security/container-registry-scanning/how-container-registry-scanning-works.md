---
description: >-
  Learn how Cortex XSIAM discovers, scans, and evaluates container images in
  onboarded registries to identify and continuously monitor security risks.
---

# How Container Registry Scanning Works

Container Registry Scanning continuously monitors container images in your onboarded registries for security risks. After you onboard a registry, Cortex XSIAM automatically discovers new and updated images, scans them, and evaluates the results against the latest threat intelligence.

The process of container registry scanning consists of three key phases:&#x20;

1. **Discovery**: The connector automatically discovers registries, repositories, and image tags across the onboarded account.&#x20;
2. **Scanning**: The connector scans newly discovered or updated images and extracts software bills of materials (SBOMs), secrets, and malware indicators. To reduce bandwidth and compute usage, the connector scans immutable container images only once. The connector rescans an image if the scanning engines are updated or if the previous scan failed.
3. **Evaluation**: Extracted artifact metadata is evaluated against current threat intelligence to identify vulnerabilities, secrets, and malware. Findings and risk scores are re-evaluated dynamically whenever new CVE data is published, without needing to re-download or rescan the container image.
