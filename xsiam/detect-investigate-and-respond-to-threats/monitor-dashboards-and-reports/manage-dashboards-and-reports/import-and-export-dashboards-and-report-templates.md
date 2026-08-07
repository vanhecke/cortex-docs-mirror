# Import and export dashboards and report templates

Administrators can export and import dashboards and report templates as JSON files. This allows you to quickly share configurations, back up content, or migrate settings between different environments. The system supports both single and bulk operations.

To perform these actions, navigate to the **Dashboard Manager** for dashboards, or the **Reports** page for report templates.

{% hint style="warning" %}
**Risk of data loss:** Importing a dashboard or report might overwrite the current version. To prevent accidental data loss, review your existing dashboards and report templates before proceeding with an import.
{% endhint %}

### Exporting dashboards & report templates

Before exporting, review the following requirements and system behaviors:

* **Infrastructure restrictions:** You cannot export dashboards built on custom infrastructure.
* **Access requirements:** To export a **Restricted** dashboard or report, you must have at least **Viewer** permissions.
* **Ownership & permissions stripping:** The exported JSON file contains only the configuration of the dashboard or template. It does not include the original access list or ownership data.

### Importing dashboards & report templates

When you import a JSON configuration, the system applies the following default rules:

* **Ownership:** You are automatically designated as the **Owner** of the imported dashboard or template.
* **Visibility:** Access is automatically set to **Restricted**. You must manually adjust the visibility settings if you want to share it. For more information, see [Visibility settings](../access-and-visibility-for-dashboards-and-reports/visibility-settings).

### Troubleshooting "No Data" messages (XQL & Datasets)

Because dashboards rely on XQL (Cortex Query Language) to fetch data, imported widgets may display a **No Data** message if they reference datasets or log sources that do not exist in your environment.

**How to fix it:**

1. Edit the affected dashboard.
2. Locate the broken widgets and edit the XQL query.
3. Update the query syntax to match the exact dataset or log source names used in your current instance.
