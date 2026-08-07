# Review all cases

The main **Cases** page is the starting point for monitoring and managing all cases in your environment. It provides visibility into all cases and their current status, helping you track progress, investigate individual cases, and take remediation actions. Severity indicators, scores, and starred icons help you quickly identify your high-priority cases.

When cases are configured with SLAs, the page helps you monitor SLA adherence and ensure cases progress in line with organizational objectives.

You can access the **Cases** page from **Cases & Issues → Cases**. By default, all open cases are displayed.

### **Viewing modes**

You can control how data is displayed and how the page behaves by choosing both a display mode and a viewing format.

* **Display modes (layout)**: You can choose how to visualize and interact with data on the page. Click the **Display** menu to switch between modes. Any changes that you make to the case fields persist between modes.
  *   **Split view (default)**

      Displays cases in a split-pane layout that highlights key details and enables you to quickly compare cases, prioritize urgent items, and assess severity and impact at a glance.
  *   **Table view**

      Displays cases in a table layout with widgets that summarize the table data. Widgets are customizable, allowing you to tailor the table for structured analysis and review.
* **Viewing formats (behavior)**: You can choose how the page functions. To change format from the **Actions** menu select **Switch to xx view**.
  *   **Default mode**

      Use the latest experience with full support for new features and functionality.
  *   **Legacy mode**

      Use the previous experience for backward compatibility. This mode does not support all newly released functionality. The documentation in this guide describes the product in **default mode**. If you are using **legacy mode**, see [Detailed View](analyze-case-details/detailed-view).

      <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Administrators can enable or disable legacy mode. Go to <strong>Configurations</strong> → <strong>General</strong> → <strong>Server Settings</strong> → <strong>Case display modes</strong>.</p></div>

### **Saved table views**

Saved table views are saved filter configurations of table data that help you to focus on the data that most matters to you. You can filter your table data by domain, context, work queue, or other criteria, and save configurations that support your workflow.

The default view on the Cases page is **All Cases**. Click on the arrow next to **All Cases** to see all available saved views. If you change the table filters, you will see a **Modified** label next to the view name. You can create a new saved views. Once you have change the table filters, click the three dots next to the view name to save the new configuration, update an existing saved view, or revert to the original configuration.

### **MSSP and multi-tenant administrators**

For MSSP and multi-tenant administrators, if the Unified Case View is enabled, this view consolidates all cases across your distributed environment, allowing you to view and perform actions on child tenants. If the Unified Case view is disabled, this view displays a single tenant at a time with a drop-down list for moving between tenants in read-only mode.

You can enable this setting from **Settings → Configurations → General → Server Settings → Unified Case View**.

For more information see [Unified case view](additional-case-actions/unified-case-view).
