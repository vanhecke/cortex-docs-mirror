# Overview of the Issues page

The **Issues** page consolidates all non-informational issues from your detection sources. By default, the **Issues** page displays the security issues received over the last seven days. To access the **Issues** page, go to Cases & Issues → Issues.

Each issue is linked to one or more cases. A case provides the full story of a problem by linking related issues, assets, and artifacts in one place. To make sure that you understand the full picture of how an issue fits into the bigger picture, we recommend that you start your investigation from the **Cases** page. You can see the issues linked to a case in the **Issues & Insights** tab of the selected case. Click on an issue to open the Issue card. For more information, see [Issue card](issue-card).

For issues associated with the Health domain, these issues are not linked to cases and should be investigated individually. You can also see Health domain issues on the **Health Issues** page. For more information, see [About health issues](../../../configure-cortex-xsiam/cortex-xsiam-data-sources/administration-and-troubleshooting/about-health-issues).

{% hint style="info" %}
### Note

Every 12 hours, the system enforces a cleanup policy to remove the oldest issues once the maximum limit is exceeded. The default issue retention period in Cortex XSIAM is 186 days.
{% endhint %}

### **Saved table views**

On the **Issues** page, you can change the displayed information by changing the table view. When you open the page, the **Security Domain** table view is displayed. Click the displayed table view to see your predefined and custom table views. You can create custom table views from scratch or by editing the predefined options.

![Saved\_views.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-31bbda8bc8afb6e4ac80d912fce92d3abd7537f1%2F11911f92958b6af3cdc88e5bef747852a9a1718d3eade9c47f3e1e6f62ce8179.png?alt=media)

<details>

<summary>Standardized format of user names in issues</summary>

Names of users are processed and displayed the in the following standardized format, also termed “normalized user”.

_**`<company domain>`**_**`\`**_**`<username>`**_

As a result, any issue triggered based on network, authentication, or login events displays the **User Name** in the standardized format in the **Issues** and **Cases** pages. This impacts every issue for Cortex XSIAM Analytics and Cortex XSIAM Analytics BIOC, including Correlation, BIOC, and IOC issues triggered on one of these event types.

</details>

<details>

<summary>Deduplicated FW issues</summary>

To reduce noise in your environment, if firewall issues with the same name and host are raised within 24 hours, the issues are deduplicated. A label indicates the number of deduplicated issues up to 1,000 issue counts, larger quantities display as 1000+.

For more information, see [Issue deduplication](issue-deduplication).

</details>

<details>

<summary>Featured fields</summary>

You can highlight issues that are important to you by tagging speciﬁc issue attributes, such as host names, user names, IP addresses, and Active Directory, as featured fields. This can help you track issues. For more information, see [Create a featured field](issue-investigation-actions/create-a-featured-field).

</details>

<details>

<summary>Issue fields</summary>

To see a full list of issue fields and descriptions, run the following query in the **Query Builder**:

```programlisting
datamodel dataset = issues
```

</details>
