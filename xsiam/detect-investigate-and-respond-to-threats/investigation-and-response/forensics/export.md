# Export

You can export the data collection for long-term retention or offline analysis.

From the collections page, choose a search item from a hunt collection or the endpoint from a triage collection and click the export icon (![forensics\_export\_icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-8597f2b6149d2a514968844ad0dfcd1a711e319d%2F1167e1677f31df5d5115e75e74973a7c2cef5383aea31c9879a005a41983aa6b.png?alt=media)). For export of all items, select the **Export All** option from the **Exports** button at the top of the **Collections** page.

{% hint style="info" %}
You can export a collection more than once.
{% endhint %}

To view the status of the export, click the **Exports** button.

The **Investigation Exports** table displays the status of the requested exports for the selected collection. The compressed export data expires from the bucket after 30 days.

<table><thead><tr><th width="158">Field</th><th>Description</th></tr></thead><tbody><tr><td>Collection name</td><td>Displays the name of the triage or hunt. For triage, the endpoint name of the triaged host is displayed.</td></tr><tr><td>Exported</td><td>Displays the time when the exported package was created (compressed).</td></tr><tr><td>Exported by</td><td>Displays the name of the user who requested the export.</td></tr><tr><td>Export expiration</td><td><p>Displays the timestamp of when the bucket data (compressed data) will be deleted.</p><p>The timestamp changes to red after the timestamp and the last column shows <em>Expired</em>.</p></td></tr><tr><td>Status</td><td>Indicates how many tables from the collections have been successfully exported to a bucket.</td></tr><tr><td>Download button</td><td>Enables you to download the the compressed (zip) export of the collection.</td></tr><tr><td>Bin icon</td><td>Enables you to delete the compressed export file.</td></tr></tbody></table>
