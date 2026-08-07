# SaaS causality view

The SaaS causality view provides a powerful way to analyze and investigate software-as-a-service (SaaS) related issues for audit stories, such as Office 365 audit logs and normalized logs, by highlighting the most relevant events and issues associated with a SaaS-related issue. To help you identify and investigate SaaS-specific data associated with SaaS-related issues and SaaS audit logs, Cortex XSIAM displays a SaaS causality view, which enables you to swiftly investigate a SaaS issue by displaying the series of events and artifacts that are shared with the issue.

A SaaS causality view is only available when Cortex XSIAM is configured to collect SaaS audit logs and data. For example, this is possible by configuring an Office 365 data collector or Google Workspace data collector with the applicable SaaS audit logs. This enables you to investigate any Cortex XSIAM issue generated from any IOC, BIOC, or correlation rules, including SaaS events. The SaaS causality view is available from the **Issues** table, or from the **Query Results** after running a query on the SaaS related data. From both places, you can right-click to pivot to the SaaS causality view.

The scope of the SaaS causality view is the Causality Instance (CI) of an event to which this issue pertains. The SaaS causality view presents the event identity and /or IP address and the actions performed by the identity on the SaaS resource. On each node in the CI chain, Cortex XSIAM provides information to help you understand what happened around the event.

The SaaS causality view contains the following sections:

<details>

<summary>Information Overview</summary>

Summarizes information about the issue you are analyzing, including the type of SaaS provider, project, and region on which the event occurred. Select **View Raw Log** to view the raw log as provided by the SaaS provider in JSON format.

</details>

<details>

<summary>SaaS causality instance chain</summary>

Includes the graphical representation of the SaaS Causality Instance (CI) along with other information and capabilities to enable you to conduct your analysis.

The SaaS causality view presents a single event CI chain. The CI chain is built from Identity and Resource nodes. The Identity node represents for example keys, service accounts, and users, while the Resource node represents for example network interfaces, storage buckets, or disks. When available, the chain can also include an IP address and issues that were triggered on the Identity and SaaS resource.

* **Identity node:** Displays the name of the identity, generated issue information, and if available the associated IP address.
* **IP address node:** Displays the IP address associated with the Identity.
* **Resource node:** Displays the referenced resource on which the operation was performed. Cortex XSIAM displays information on the following resources.

**Navigation**

You can move the chain, extend it, and modify it. To adjust the appearance of the CI chain, use the size controls on the right. You can also move the chain by selecting and dragging it. To return the chain to its original position and size, click ![causality-view-reset-icon.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-02413f496b1c767ec7cb02225bc1e0e6c8b66b8b%2Fdb69f0a560c666334cf243831344778fcda2e5341654ae3631d61bc10b019357.png?alt=media) in the lower-right of the CI graph.

#### To further investigate the user

1. Hover over an Identity node to display, if available, the identity Analytics Profiles.
2. Select the Identity node to display in the Entity Data section additional information about the Identity entity.
3. Select the issue icon to display additional information in the Forensics Highlights tab.

#### To further investigate the resource

1. Hover over a Resource node to display, if available, the resource Analytics Profiles and Resource Editors statistics.
2. Select the Resource node to display in the Entity Data section additional information about the Resource entity.

</details>

<details>

<summary>All Events table</summary>

Displays up to 100,000 related events and up to 1,000 related issues. In the **All Events** table, Cortex XSIAM displays detailed information about each of the related events. To simplify your investigation, Cortex XSIAM scans your Cortex XSIAM data aggregating the events that have the same Identity or Resource and displays the entry with an <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a2f001ce9456c1424ca2b48c506a1e02056763f3%2F862436a5df1eb6af965121c50352fb99efa8bc5af597dd078606e6db8cd7a573.png?alt=media" alt="cloud-causality-aggregated-events.png" data-size="line"> aggregated icon. Right-click and select **Show Grouped Events** to view the aggregated entries.

Entries highlighted in red indicate that the specific event created an issue. To continue the investigation, right-click to **View in XQL**. To continue the investigation, in the **Issues** table, right-click an issue to see the available actions.

</details>

<details>

<summary>Key of SaaS resources</summary>

The following table lists the SaaS resource icons:

<table><thead><tr><th width="122">Icon</th><th>Type of resource</th></tr></thead><tbody><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-82880300c1e7caa8c9da7ba1bf3029b8a5e158c4%2Fda0972ba4cfa4c367e5053aeb1375429d3368057798923337a796fe50ba52ff1.png?alt=media" alt="saas-resource-1.png"></td><td>Google Workspace Admin Console</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-19d41ce9b1e2ea9fdc61175243c3fa992dcf5f1b%2Fa6f57f0f201a85b39cb9000b10b97a59f1d6dc74cb666e806e19331aee1f7339.png?alt=media" alt="saas-resource-2.png"></td><td>Google Workspace for Google Drive</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f0bf030afc49bc5cca92206c8be61917e18900f5%2Fc07a2f4586f189b6dd9e419aaf64b67b5945276b1b48b14c7b20d40ced3c81ff.png?alt=media" alt="saas-resource-3.png"></td><td>Microsoft Office 365 Exchange Online</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-98dd13f1e634cacf96a2757b0409a6630a4934bb%2F1baa3e50eca73f03c01d80eb7250258d4635ba035fd54b75427f9d9acb0da422.png?alt=media" alt="saas-resource-4.png"></td><td>Microsoft 365 Office Groups</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-726a7c7e1122a20ad505e1acd6e157115550dabe%2F3179fa0c2cc19aee4b1516891b08bc5b54180362ff61688f5de565b56ca17e07.png?alt=media" alt="saas-resource-5.png"></td><td>Microsoft Office 365 OneDrive</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f01584c1dff9917463c129e669f25b5dc5c22c22%2F3938054cab4146694800f5651869f0454506e23b767a044956df247e8cd727f1.png?alt=media" alt="saas-resource-6.png"></td><td>Microsoft Office 365 SharePoint Online</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-98e4dca96d304ddf6a9051e73c52c4610b7d5ba9%2Fa7c3500f323ef001a923aa89e1db1f3bb9fcf73c2c8c0741d7ea7c2115a17b5d.png?alt=media" alt="saas-resource-7.png"></td><td>Microsoft Office 365 Skype for Business</td></tr><tr><td><img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-de5d65ca488e8bb043cf788f8ff6896afe70ab58%2F5a5e572ee4a62f0b26d15222c4750c752446431a7f2c547f08d3c838f55da0fa.png?alt=media" alt="saas-resource-8.png"></td><td>Microsoft Office 365 Teams</td></tr></tbody></table>

</details>
