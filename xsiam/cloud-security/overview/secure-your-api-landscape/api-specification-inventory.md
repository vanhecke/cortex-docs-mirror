# API specification inventory

Cortex XSIAM offers the option to import API specifications that comply with the [OpenAPI](https://www.openapis.org/) format, including format, file structure, and data types.

In addition to observing API traffic, Cortex XSIAM scans AWS and Azure API gateways, and extracts the API specification files. Once the specification files are in the inventory, Cortex XSIAM scans them for misconfigurations and vulnerabilities, providing insights into your API landscape.

Use Cortex XSIAM to validate live traffic against specifications and alert on surface deviations, undocumented endpoints, or security gaps.

The following table describes the fields that are available for each API specification.

| Field                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sources              | <p>Source of the API specification:</p><ul><li>User</li><li>API Gateway Configuration</li></ul>                                                                                                                                                                                                                                                                                                                                                                      |
| Asset Name           | Asset name is obtained from the `title` field in the specification.                                                                                                                                                                                                                                                                                                                                                                                                  |
| Servers List         | <p>This field is automatically filled if the specification contains the server URL or host. You must manually add the URL or host address if there is no URL or host in the specification.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>Even if you have already imported the specification, you can edit the API specification in Cortex XSIAM and add or update the server list.</p></div> |
| API Versions         | API version obtained from the API specification.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Associated Endpoints | <p>Shows the number of endpoints that match the specification.</p><p>You can right-click and select <strong>View Associated Endpoints</strong> to see the matched paths in the <strong>API Endpoints</strong> table.</p>                                                                                                                                                                                                                                             |
| Format & Version     | OpenAPI or Swagger and the relative version.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Spec File Name       | Specification file name that was imported to Cortex XSIAM.                                                                                                                                                                                                                                                                                                                                                                                                           |
| Findings             | The total number of findings is broken down by severity, and findings with a severity of high trigger an issue.                                                                                                                                                                                                                                                                                                                                                      |
| Status               | <p>Indicates if the specification is:</p><ul><li>Unknown</li><li>Active</li><li>Recently Active</li><li>Inactive</li><li>Deleted</li></ul>                                                                                                                                                                                                                                                                                                                           |

Click the API asset to open the side card. Each tab includes detailed information from the parsed data of the API.

You can add **Comments** (![api\_specification\_comments.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a7974396089336a16748c961bb598870194f6ddb%2Fca0e3eb2f6b905ef9e0e2310ae50eb4c4381088e1cef935638625ed4d1be7325.png?alt=media)) to the specification, providing additional context about the API endpoints or other relevant information.

<details>

<summary>Overview</summary>

Shows the highlights and properties of the API endpoint asset.

| Field                 | Description                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Asset ID              | API asset ID.                                                                                                                                                                                                                                                                                                                                                                           |
| Provider              | <p>Gateway provider:</p><ul><li>GCP</li><li>AWS</li><li>Azure</li><li>On Prem</li></ul>                                                                                                                                                                                                                                                                                                 |
| Asset Category        | API Endpoint or API Specification                                                                                                                                                                                                                                                                                                                                                       |
| Account ID            | Account ID of the API specification.                                                                                                                                                                                                                                                                                                                                                    |
| Asset Groups          | Indicates the asset group that the API is associated with. For more information, go to [Asset groups](../../../detect-investigate-and-respond-to-threats/asset-management/asset-groups).                                                                                                                                                                                                |
| Cases/Issues/Findings | <p>The page shows issues and cases.</p><p>The link from the number opens the page where you can review the details. Refer to <a href="../../../detect-investigate-and-respond-to-threats/investigation-and-response/overview-of-cases/what-are-cases">Cases and issues</a> for detailed information.</p><p>You can view all API security issues and cases detected by Cortex XSIAM.</p> |
| Evidence              | Shows findings that provide visibility into the risks and vulnerabilities of your API landscape. By continuously analyzing findings, you can maintain an up-to-date view of the API asset’s security posture and support more informed decision-making for detection, prioritization, and remediation efforts.                                                                          |

An issue is generated when the following **Detection Method** is triggered.

| Deployment option     | Detection Method and Type                 | Description                                                                                                                                                                                                                      |
| --------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agentless for Posture | **Detection Method**: API Posture Scanner | <p>If Cortex XSIAM detects security vulnerabilities or compliance issues in the posture of an API during scanning, an issue is generated.</p><p>The issue includes specification static scan findings relevant to the issue.</p> |

</details>

<details>

<summary>Code</summary>

The schema shows the actual API specification that includes the basic information of the API, the API path, method, and parameters.

</details>

<details>

<summary>Insights</summary>

At a glance, we see a graphical representation of the specification scan results by severity and by category.

You can filter in by severity or by category. Drill down to view details of the selected scan result.

The specification scan results by severity table include the following information:

| Field             | Description                                                                                                                                                                                           |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Severity          | Indicates the severity of the scan result issue.                                                                                                                                                      |
| Category          | <p>API category. The options are:</p><ul><li>Access Control</li><li>Networking and Firewall</li><li>Insecure Configurations</li><li>Data</li><li>Encryption</li><li>Structure and Semantics</li></ul> |
| Name              | Name of API specification.                                                                                                                                                                            |
| Description       | Details of the scan results.                                                                                                                                                                          |
| Modification Time | Time stamp of when the API specification was modified                                                                                                                                                 |
| Finding ID        | For every vulnerability, a finding is created.                                                                                                                                                        |

You can drill down by clicking a severity to see the details/information of the findings (vulnerabilities).

| Field                  | Description                                                                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Severity               | <ul><li>Critical/High/Medium/Low</li><li>Info</li></ul>                                                                                    |
| Category               | API category.                                                                                                                              |
| Link to OpenAPI checks | .[OpenAPI](https://www.openapis.org/) page of the scan results item includes a description of the issue and a link to **Details** You can: |
| Description            | Details of the scan results.                                                                                                               |
| Scan Result Issue      | Refers to the number of findings.                                                                                                          |
| Scan Results           | Shows the findings in the API request. The issue is highlighted.                                                                           |

</details>

**Import API specification**

Cortex XSIAM enables you to import YAML or JSON files. After importing the file, Cortex XSIAM analyzes the data to identify vulnerabilities to help you effectively manage and enforce security measures.

**How to import an API Specification**

1. Go to Inventory → All Assets → APIs → **Specification**.
2. Click **Import API Specification**.
3.  Drop or browse for the API specification file and add the server of where the file is hosted. This field is automatically filled if the file contains the server URL or host. If there is no URL or host in the file, you must manually add the URL or host address.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Even if you already imported the file, you can edit the API asset and add or update the server list.</p></div>
4.  Click **Import**.

    It can take up to 30 minutes to import the file.
