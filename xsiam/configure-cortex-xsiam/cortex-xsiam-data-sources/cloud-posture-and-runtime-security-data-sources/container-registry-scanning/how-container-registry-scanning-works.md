---
description: >-
  Learn how Cortex XSIAM scans container registries and evaluates container
  image risks.
---

# How Container Registry Scanning Works

The process of container registry scanning consists of three key phases: discovery, scanning, and evaluation.

1. **Discovery**: The connector discovers all registries, repositories, and tags within the account.
2. **Scanning**: The connector extracts software bills of materials (SBOMs), malware indicators, and secrets from each image.
3. **Evaluation**: Scan results are evaluated for vulnerabilities, malware, and secrets, and asset findings are created accordingly.
