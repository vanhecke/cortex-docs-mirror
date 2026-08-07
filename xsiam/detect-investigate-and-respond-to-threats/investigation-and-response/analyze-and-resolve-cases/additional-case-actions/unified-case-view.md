# Unified case view

{% hint style="info" %}
### License

Requires an MSSP license.
{% endhint %}

{% hint style="info" %}
### Note

* Requires the following RBAC permissions:
  * **Cases & Issues**
  * **Investigation & Response** → **Automation**
* This view is available for the parent tenant only.
* To take actions on a child tenant from a parent tenant, you must have the appropriate permissions for both tenants. If you do not have the correct permissions, you can view cases in read-only mode.
{% endhint %}

For MSSP and multi-tenant administrators, the **Unified Case View** provides a central location to view and perform actions on child tenants across your distributed environment. You can see a consolidated view of all cases, easily visualize and triage the cases in your environment, and collaborate with child users.

You can access the **Unified Case View** from **Cases & Issues** → **Cases**.

In the **Tenant Name** column you can see the name of the parent and child tenants. Use this field to filter the table and see cases from a specific child tenant. When you investigate a case on a child tenant Cortex XSIAM pivots into the child tenant screen so that you can perform actions directly in the case, and run commands in the **War Room**.

In addition, you can take bulk actions across multiple tenants, such as changing the status and severity, and running playbooks. When running a playbook on an issue, you can select from the playbooks that are available in the child tenant. The **Tenant Name** column is also displayed on the **Issues** page, and enables pivoting to the child tenant.

{% hint style="info" %}
### Note

Custom case layouts of child tenants are not visible in the parent tenant.
{% endhint %}

### **Limitations**

To ensure a streamlined user experience in the **Unified Case View**, we want to make you aware of the current unsupported functionalities that we are working to improve in the upcoming releases:

* **Cases** → **Table view**
  * **Tags**, **Original Tags**, and Custom fields are not supported and therefore are not displayed in the table.
*   Access Control

    When viewing the **Unified Case View**, SBAC on the Parent Tenant is not enforced.

As a fallback option, you can disable the **Unified Case View** from **Settings** → **Configurations** → **Server Settings** → **Unified Case View**.
