# Limitations & supported regions

**Service limitations**

* **Unsupported features**: FedRAMP Government instances do not currently support these DSPM services:
  * AWS: RDS/Aurora scanning
  * DBaaS: Snowflake, Databricks
  * Microsoft 365
  * Azure: All services (**this is not supported for both DSPM and AISPM services**)
* **Environmental restrictions**: Multi-tenant or MSSP environments are not currently supported by FedRAMP.
* **Permitted capabilities**: Other capabilities, such as registry scanning, serverless scanning, and agentless disk scanning, are allowed.

**Supported regions**

Supported regions are limited to AWS GovCloud regions and Microsoft Azure government regions.

| Provider          | Supported regions                                                                                                                                                |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AWS GovCloud      | <ul><li>AWS GovCloud (US-East) - <code>us-gov-east-1</code></li><li>AWS GovCloud (US-West) - <code>us-gov-west-1</code></li></ul>                                |
| Azure Governement | <ul><li>US Gov Arizona - <code>usgovarizona</code></li><li>US Gov Texas - <code>usgovtexas</code></li><li>US Gov Virginia - <code>usgovvirginia</code></li></ul> |
