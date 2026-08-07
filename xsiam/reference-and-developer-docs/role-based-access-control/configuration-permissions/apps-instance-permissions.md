# Apps - Instance permissions

Controls the ability to install, configure, and delete Jupyter Notebooks and Observability instances (Settings → Configurations → Integrations → Apps).

To use and access the apps, users need the Apps permission. For more information, see [Jupyter and Observability apps permissions](../jupyter-and-observability-apps-permissions).

| Permission | Description                                                                                             | Role Example                                                                               |
| ---------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| None       | Users cannot see the Apps page.                                                                         | SOC Tier-1, 2, and 3 Analysts, and Threat Hunter: Should not manage application instances. |
| View       | Users can view the list of available and installed apps, but cannot install, configure, or delete them. |                                                                                            |
| View/Edit  | Full control over the Apps page, including installing, configuring, and deleting app instances          | Security Engineer: Deploy and manage applications.                                         |

Required and recommended permissions

As Apps like Jupyter and Observability interact with datasets and infrastructure, consider adding these dependencies:

| Permissions          | Permission Level  | Reason                                                                 |
| -------------------- | ----------------- | ---------------------------------------------------------------------- |
| Apps (Jupyter)       | View or View/Edit | Required to access Jupyter notebook instances after they are created.  |
| Apps (Observability) | View or View/Edit | Required to access Observability app instances after they are created. |
| Query Center         | View              | Strongly recommended for XQL queries within Jupyter notebooks          |
| Credentials          | View              | Recommended to access datasets from within Jupyter for analysis.       |

<details>

<summary><strong>Cortex SDK permission requirements for Jupyter Notebooks</strong></summary>

When using Jupyter Notebooks with the Cortex SDK (Python SDK for Cortex XSIAM), the effective permissions are determined by the API Key configured for the Jupyter instance. The Cortex SDK authenticates with XSIAM APIs using this API key, and the key's associated RBAC role determines which data and actions are accessible within notebooks.

API key configuration

When configuring a Jupyter instance, an API key must be selected. This API key determines:

| Aspect              | Description                                         |
| ------------------- | --------------------------------------------------- |
| Authentication      | SDK uses the API key for all XSIAM API calls.       |
| RBAC role           | The API key's assigned role determines permissions. |
| Dataset access      | Only datasets permitted by the role are queryable.  |
| Action capabilities | Response actions limited to role permissions        |
| Scope               | Optional scope restrictions further limit access.   |

API keys can have different security levels that affect SDK authentication:

| Security level | Description                                      | Use case                |
| -------------- | ------------------------------------------------ | ----------------------- |
| Standard       | Basic authentication                             | Development, testing    |
| Advanced       | Enhanced authentication with nonce and timestamp | Production environments |

Best practices for Jupyter and Cortex SDK

*   Principle of least privilege

    Create a dedicated API key for Jupyter with minimal required permissions. Avoid using admin-level API keys for notebook operations, and regularly audit API key usage and permissions.
*   Dataset access control

    Limit dataset access to only those needed for analysis. Consider creating a dedicated RBAC role for Jupyter SDK operations and using scope restrictions to limit data visibility.
*   Action permissions

    Only enable response action permissions if notebooks will execute remediation. Consider separate API keys for read-only analysis vs. active response, and log and monitor all SDK-initiated actions.
*   API key management

    Set appropriate expiration times for API keys. Rotate API keys periodically, and use descriptive comments to identify Jupyter-associated keys.

Key permissions for Cortex SDK operations

| Permission          | Permission Level                 | Reason                                                                                                                                                                                                                                                                                        |
| ------------------- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query Center        | View or View/Edit                | <ul><li>View: Required to run XQL queries through the SDK</li><li>View/Edit: Strongly recommended to create/save queries.</li></ul>                                                                                                                                                           |
| Query library       | Enabled                          | <ul><li>Enabled: Strongly recommended to access saved queries</li><li>Enabled with checkboxes selected: Recommended to save queries to the Query library.</li></ul>                                                                                                                           |
| Dataset permissions | N/a                              | <p>Configured per-role when creating a role. Select</p><ul><li>Raw dataset: Required, Access to raw log data</li><li>Correlation dataset: Strongly recommended to access the correlation data.</li><li>User/audit datasets: Recommended to access user-related data and audit logs.</li></ul> |
| Cases & Issues      | View or View/Edit                | <ul><li>View: Strongly recommended to query case/issue data.</li><li>View/Edit: Recommended for automated workflows.</li></ul>                                                                                                                                                                |
| Action Center       | View/Edit                        | <p>If the role includes action permissions, the SDK can execute response actions. Recommend adding:</p><ul><li>Isolate: Isolate endpoints</li><li>Terminate process: Terminate processes via SDK</li><li>File retrieval: Retrieve files</li><li>Quarantine files</li></ul>                    |
| Threat Intel        | View                             | Strongly recommended to enrich data with threat intelligence. When creating/editing a role, select Threat Management. See [Threat Management permissions](../threat-management-permissions).                                                                                                  |
| Scripts/playbooks   | Enabled with checkboxes selected | Recommended for engineering workflows.                                                                                                                                                                                                                                                        |

</details>
