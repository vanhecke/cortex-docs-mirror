# Verify collector connectivity

You can verify the connectivity status of a collector instance on the Data Sources & Integrations page. Instances are grouped by integration, and the **Instances Status** column shows icons that summarize the instance statuses for the integration. Click the integration to see details for each individual instance.

In addition, Cortex XSIAM creates Collection health issues if connectivity disruptions occur in your collection integrations, custom collectors, and Marketplace integrations. For more information, see [About health issues](about-health-issues).

**Troubleshooting collector errors**

{% hint style="info" %}
### Note

For more information on troubleshooting data collector applet errors, see Troubleshoot Broker VM applet connectivity.
{% endhint %}

<details>

<summary>Where can I see if I have a connectivity error on a collector instance?</summary>

On the Data Sources & Integrations page, instances in error status display an error icon. Hover over the error icon next to the instance name to see the error message as received from the API.

</details>

<details>

<summary>Where can I trace the connectivity changes of a collector instance?</summary>

Each status change of an instance is logged in the `collection_auditing` dataset. Querying this dataset can help you see all the connectivity changes of an instance over time, the escalation or recovery of the connectivity status, and the error, warning, and informational messages related to status changes.

This example searches for status changes on Strata IOT integrations:

```programlisting
dataset = collection_auditing 
|filter collector_type = "STRATA_IOT"
```

</details>

<details>

<summary>How can I set up correlation rules to trigger collection issues?</summary>

Cortex XSIAM provides OOTB Collection issues that are triggered when a data collector instance is in error status, which means it is disconnected or not sending data. In addition, you can set up your own correlation rules that trigger collection issues for your specific needs. For example, you might want to be notified if a high-profile collector is in warning status so that you can fix the problem and prevent the collector from disconnecting.

Example: Trigger collection issues for warning statuses on the STRATA\_IOT collector

In this example, a correlation rule triggers a Collection issue if an integration of the Strata IOT collector changes to warning status. Any issues will appear on the **Health Issues** page.

Example XQL:

```programlisting
dataset = collection_auditing 
|filter classification = "Warning" and collector_type = "STRATA_IOT"
```

Additional fields to specify in the correlation rule:

| Field             | Value                                                                                                                                                                                                                                                                                                                                              |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Time Schedule     | Hourly                                                                                                                                                                                                                                                                                                                                             |
| Query time frame  | 1 Hour                                                                                                                                                                                                                                                                                                                                             |
| Issue Suppression | Select **Enable issue suppression**.                                                                                                                                                                                                                                                                                                               |
| Action            | Select **Generate issue**.                                                                                                                                                                                                                                                                                                                         |
| Issue Domain      | Health                                                                                                                                                                                                                                                                                                                                             |
| Severity          | Medium                                                                                                                                                                                                                                                                                                                                             |
| Category          | <p>Collection</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>If an issue is triggered, the investigation options in the right-click menu of the <strong>Health Issues</strong> pages are context-specific. Make sure that you specify the relevant issue category.</p></div> |

</details>
