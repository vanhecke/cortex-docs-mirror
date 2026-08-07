# Ingest data from ServiceNow CMDB

To receive data from the ServiceNow CMDB database, you must first configure data collection from ServiceNow CMDB. ServiceNow CMDB is a logical representations of assets, services, and the relationships between them that comprise the infrastructure of an organization. It is built as a series of connected tables that contain all the assets and business services controlled by a company and its configurations. You can configure the Collection Integration settings in Cortex XSIAM for the ServiceNow CMDB database, which includes selecting the specific tables containing the data that you want to collect, in the ServiceNow CMDB Collector. You can select from the list of default tables and also specify custom tables. By default, the ServiceNow CMDB Collector is configured to collect data from the following tables, which you can always change depending on your system requirements.

* `cmdb_ci`
* `cmdb_ci_computer`
* `cmdb_rel_ci`
* `cmdb_ci_application_software`

When Cortex XSIAM begins receiving data, the app automatically creates a ServiceNow CMDB dataset for each table using the format `servicenow_cmdb_<table name>_raw`. You can then use XQL Search queries to view the data and create new Correlation Rules.

You can only configure a single ServiceNow CMDB Collector, which is automatically configured every 6 hours, to reload the data from the configured tables and replace the existing data. You can always use the Sync Now option to reload the data and replace the existing data whenever you want.

Complete the following task before you begin configuring Cortex XSIAM to receive data from ServiceNow CMDB.

* Create a ServiceNow CMDB user with SNOW credentials, who is designated to access the tables from ServiceNow CMDB for data collection in Cortex XSIAM. Record the credentials for this user as you will need them when configuring the ServiceNow CMDB Collector in Cortex XSIAM.

Configure Cortex XSIAM to receive data from ServiceNow CMDB:

1. Navigate to Settings → Data Sources & Integrations.
2. On the Data Sources & Integrations page, click + Add New, search for ServiceNow CMDB, then hover over it and click Add.
3. Set the following parameters.
   * Domain: Specify your ServiceNow CMDB domain URL.
   * User Name: Specify the username for your ServiceNow CMDB user designated in Cortex XSIAM.
   * Password: Specify the password for your ServiceNow CMDB user designated in Cortex XSIAM.
   * Tables: You can do any of the following actions to configure the tables whose data is collected from ServiceNow CMDB.
     * Select the tables from the list of default ServiceNow CMDB tables that you want to collect from. After each table selection, select [![blue-arrow.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAAQCAYAAADwMZRfAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH4wsVCBYT2ibwgQAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAAAhElEQVQ4jWP8////fwYKAROlBgy8IeuuMDC8+kIFl/z9j8OQhx8YGO68Jc0wFEPefGVgOPsEQpMCWGCMX38ZGE48YmDgYmVg4GVnYLj+igxDvv+GGMTIwMBw8zVxmrlY0Qzh52BgkBeAhImxDIRNLEAJE5jmh++JN4CBgYGBcTTZ08YQANciJquKoM3CAAAAAElFTkSuQmCC)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/83ab~W8kgCI6NcvEhUNjtg-5CAbsl8idaK8R43ZLhoTOw) to add the table to the tables already listed below for data collection.
     * Specify any custom tables that you want to configure for data collection.
     * From the default list of tables already configured, you can delete any of them by hovering over the table and selecting the X icon.
4.  Click Test to validate access, and then click Enable.

    After events start to come in, a green check mark appears underneath the ServiceNow CMDB Collector configuration with the data and time that the data was last synced.
5.  (Optional) Manage your ServiceNow CMDB Collector.

    After you enable the ServiceNow CMDB Collector, you can make additional changes as needed. To modify a configuration, select any of the following options:

    * Edit the ServiceNow CMDB Collector settings.
    * Disable the ServiceNow CMDB Collector.
    * Delete the ServiceNow CMDB Collector.
    * Sync Now to get the latest data from the tables configured. The data is replaced automatically every 6 hours, but you can always get the latest data as needed.
6. After Cortex XSIAM begins receiving data from ServiceNow CMDB, you can use the XQL Search to search for logs in the new datasets, where each dataset name is based on the table name using the format `servicenow_cmdb_<table name>_raw`.
