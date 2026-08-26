---
description: >-
  Use Cortex XSIAM MCP Server tools to investigate assets, cases, issues, and
  endpoints, and create custom tools for security workflows.
---

# Use the Cortex MCP server

The Cortex MCP server provides built-in tools to manage cases and issues and conduct investigations.

Built-in tools include, but are not limited to:

* **get\_assets**: Fetch all assets, or a filtered subset of assets, based on criteria such as category, region, or provider.
* **get\_assets\_by\_id**: Fetch detailed information about the asset specified by the asset ID.
* **get\_cases**: Fetch all cases, or a filtered subset of cases matching specific criteria such as domain, status, severity, or a specific case ID.
* **get\_issues**: Fetch all issues, or a filtered subset of issues matching specific criteria such as domain, severity, detection method, or specific issue ID.
* **get\_assessment\_profile\_results**: Fetch the results of all or filtered compliance assessments from the Cortex platform.
* **get\_filtered\_endpoints**: Fetch a filtered list of endpoints managed by the XDR agents based on their status, XDR agent status, and other filters.

When you run the `update` command in the Cortex MCP server, new or updated tools provided by Cortex are automatically downloaded.

You also have the flexibility to create and customize your own tools to fit specific use cases and workflows. For more information, see [Create custom Cortex MCP server tools](create-custom-cortex-mcp-server-tools).

### **Cortex MCP Server use case examples**

{% hint style="info" %}
The built-in tools retrieve information, but do not write to the tenant. You can create your own tools that include write actions. The examples below include both.
{% endhint %}

* Show me the top ten most critical cases and create a graphical representation for my manager to review.
* Give me the details for case ID 12345 and create a visual timeline.
* Isolate endpoint WIN-123 because it may be compromised.
* Retrieve full details for endpoint XXXX.
* Add a note to case 12345 saying, ‘Escalated to Tier 2 for further investigation.
