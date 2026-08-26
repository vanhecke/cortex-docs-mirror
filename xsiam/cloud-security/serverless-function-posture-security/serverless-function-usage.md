---
description: >-
  Manage serverless function assets, vulnerabilities, findings, and scan health
  in Cortex XSIAM.
---

# Serverless function usage

Serverless functions is integrated as a feature across various sections of your tenant. Refer to the following sections for specific usage instructions within each context:

### Serverless function assets

The **Serverless Functions** asset inventory provides a centralized view of all serverless functions in your environment.

To access serverless function assets, under **Inventory**, select **All Assets** → **Compute** → **Serverless Functions**.

For more information on serverless function assets, refer to [Manage serverless function assets](../../detect-investigate-and-respond-to-threats/asset-management/asset-classes/compute-assets/serverless-functions-assets)

### Serverless function issues

Currently, only vulnerability issues are supported for serverless functions.

* To manage serverless function vulnerability issues through **Vulnerability Management**:
  1. Navigate to **Posture Management** → **Vulnerability Management)** → **Vulnerability Issues**.
  2. Select **Add Filters** → **Asset Category** → **Serverless Function**.
* To manage serverless function vulnerability issues through **Vulnerability Assets**:
  1. Navigate to **Posture Management** → **Vulnerability Management)** → **Vulnerable Assets**.
  2. Select **Add Filters** → **Asset Category** → **Serverless Functions**.
  3.  Select an asset in the inventory table.

      The Overview tab is displayed.
  4.  Click on **Issues**.

      You are redirected to the Issues page, displaying a list of serverless function vulnerabilities.

The serverless function vulnerabilities issues inventory includes these unique properties:

* **Asset Type**: The type of serverless function: **Lamda Function** for AWS, **Google Cloud Function** for GCP and **Azure App Service Web App Function** for Azure
* **Asset Category**: Serverless Functions

Selecting an issue opens the expanded card with additional details about the issue including a description of the issue, when fist and last detected, affected assets, linked cases and evidence (such as the vulnerability ID, CVSS severity, score and version, and the policy that detected the issue).

For more information on vulnerability issues, refer to [Investigate and remediate vulnerabilities](../../detect-investigate-and-respond-to-threats/vulnerability-management/investigate-and-remediate-vulnerabilities).

### Serverless function findings

1. To manage serverless function findings, navigate to **Posture Management** → **Vulnerability Management)** → **Vulnerability Issues**.
2. Select All Vulnerabilities Findings.
3. Select **Add Filters** → **Asset Category** → **Serverless Function**.
4. Select an asset in the inventory table.

For more information on vulnerability findings, refer to [View All Vulnerability Findings](../../../detect-investigate-and-respond-to-threats/vulnerability-management/investigate-and-remediate-vulnerabilities#view-all-vulnerability-findings).

### Monitor serverless function scan health

You can monitor and manage the health and status of your integrated serverless function scans, troubleshoot errors and mitigate detected vulnerabilities

For more information, refer to Monitor serverless function scan health.
