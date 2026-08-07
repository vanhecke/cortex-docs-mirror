# Ingestion Monitoring dashboard permissions

Access to the Data Ingestion Dashboard, which provides an overview of data ingestion by product and vendor:

* Daily quota consumption: Tracking used data limits against the organization's allowance.
* Data ingestion rates: Visualizing the velocity of incoming data.
* Source Health: Ensuring that various data sources and products are communicating correctly with Cortex XSIAM.

| Permission | Description                                       | Roles Example                           |
| ---------- | ------------------------------------------------- | --------------------------------------- |
| None       | No access to the Data Ingestion Dashboard.        |                                         |
| View       | Read-only access to the Data Ingestion Dashboard. | Most roles should have view permission. |

### Required and recommended permissions

To effectively utilize the ingestion monitoring tools, consider these dependencies:

| Permission   | Permission Level | Reason                                                                 |
| ------------ | ---------------- | ---------------------------------------------------------------------- |
| Dashboards   | Enabled          | Required to access the dashboard.                                      |
| Query Center | View             | Recommended for deeper analysis of ingestion data through XQL queries. |
