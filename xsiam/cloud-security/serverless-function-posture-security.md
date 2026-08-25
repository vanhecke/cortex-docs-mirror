---
description: >-
  Cortex XSIAM scans AWS, GCP, and Azure serverless functions for
  vulnerabilities, malware, and exposed secrets.
---

# Serverless function posture security

Cloud serverless function scanning capabilities provide comprehensive visibility into the security posture of your serverless functions across your code and CI/CD environments, without the need to install agents or disrupt your workload operations. By integrating scanning functionality directly into your serverless functions, Cortex Cloud automatically detects vulnerabilities, malware, and exposed secrets early in the development process, enabling proactive risk detection and mitigation before production.

The following events trigger Cortex Cloud serverless function scans:

* Periodic scans
* Settings modifications, including adding new functions for scanning

### Supported platforms

* Supported architecture: x86\_64
* Supported cloud providers:
  * Amazon Web Services (AWS): Lambda functions
  * Google Cloud Platform (GCP): Google Cloud Functions (1st-gen and 2nd-gen Cloud Functions API
  * Microsoft Azure: Azure Functions

### Use cases

* **Scan Serverless Functions**: You can set up automated security scans for all your serverless functions to regularly check for potential vulnerabilities, malware, and exposed secrets. You can schedule these scans to run periodically or automatically (event-driven) whenever changes are made to your functions. The scan results allow you to assess the security risks associated with your serverless applications.
* **Visibility**: Get a single view of all vulnerabilities, malware, and exposed secrets affecting your organization's serverless functions. This allows you to easily understand the overall security posture of these assets.
* **Analyze and mitigate scan results**: Gain insights about the vulnerabilities, malware and exposed secrets detected by serverless function security scans. This enables you to understand and mitigate potential risks to improve the security of your serverless applications.
* **Monitor scan health**: Gain detailed insights into serverless function scan health and status, allowing you to track scan data, troubleshoot errors and mitigate detected vulnerabilities, malware, and exposed secrets, ensuring the overall health of your serverless functions.
