# Public API

Controls access to API key management for external integrations. This includes creating, viewing, editing, and revoking API keys that allow external systems to interact with Cortex XSIAM in Settings → Configurations → Integrations → API Keys. The Public API permissions also manage access to the Compute Unit Usage page.

### Error Handling

Any API call attempting to fetch, list, or modify stored secrets using a restricted key will return a 403 Forbidden error with an Insufficient permissions message. This ensures that automated workflows, scripts, and CLI interactions follow a strict least-privilege model.

| Permission | Description                                                                                                                                                                                                                                                                                                                               | Roles Example                                                                                                                                 |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| None       | <p>The user cannot see the API Keys page or view or manage the Compute Unit Usage page.</p><ul><li><strong>Access level</strong>: 403 Forbidden</li><li><strong>Capabilities</strong>: All credential endpoints are blocked. Automated workflows, scripts, and CLI interactions cannot view, list, or reference stored secrets.</li></ul> | SOC Tier-1 Analyst: No need for API or Compute Unit Usage page access.                                                                        |
| View       | The user can view the list of existing API keys but cannot create, edit, or delete them. The user can view the Compute Unit Usage page, but cannot edit the daily compute unit limit.                                                                                                                                                     | <ul><li>SOC Tier-2 and 3 Analysts: May need to verify API integrations.</li><li>Threat Hunter: Review API integrations for hunting.</li></ul> |
| View/Edit  | The user has full control over API keys, including creating, editing, and deleting them. The user can view the Compute Unit Usage page and edit the daily compute unit limit.                                                                                                                                                             | Security Engineer: Develop and manage API integrations. Manage daily usage of compute units.                                                  |

#### Required and recommended permissions

As API keys are often used to bridge data between modules, consider the following dependencies:

| Permission   | Permission Level | Reason                                                                                                     |
| ------------ | ---------------- | ---------------------------------------------------------------------------------------------------------- |
| Audit        | View             | Strongly recommended to track API key creation, modification, and deletion events for security compliance. |
| Integrations | View             | Recommended to understand which integrations use API keys for data collection.                             |
| Credentials  | View             | Recommended to view credentials that may be associated with API-based integrations.                        |
