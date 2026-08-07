# Step 2. Define access configuations and role permissions

To set up manual pairing in a customer-owned license multi-tenant deployment, after the parent and child Cortex XSIAM tenants are activated, you must define correct access configuration in the Customer Support Portal (CSP) and role permissions in Cortex Gateway.

The following table describes the access configurations and role permissions needed:

| Tenant         | Application                                                                                                                  | Action                                                                                                                                        |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Parent         | Customer Support Portal (CSP) Account                                                                                        | Ensure the parent user name has Super User role permissions.                                                                                  |
| Cortex Gateway | Ensure the user name added to the child tenant’s CSP account has Admin role permissions on the parent Cortex XSIAM instance. |                                                                                                                                               |
| Child          | Customer Support Portal (CSP) Account                                                                                        | Add the user name from the parent tenant who is initiating the parent-child pairing and ensure the user name has Super User role permissions. |
| Gateway        | Provide the user name added in CSP with Admin role permissions to access the child Cortex XSIAM instance.                    |                                                                                                                                               |
