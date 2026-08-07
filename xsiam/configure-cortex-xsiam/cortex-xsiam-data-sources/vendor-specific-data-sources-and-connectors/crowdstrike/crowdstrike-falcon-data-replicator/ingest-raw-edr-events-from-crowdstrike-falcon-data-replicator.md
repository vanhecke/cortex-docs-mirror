# Ingest raw EDR events from CrowdStrike Falcon Data Replicator

Cortex XSIAM enables ingestion of raw EDR event data from CrowdStrike Falcon Data Replicator (FDR), streamed to Amazon S3. In addition to all standard SIEM capabilities, this integration unlocks some advanced Cortex XSIAM features, enabling comprehensive analysis of data from all sources, enhanced detection and response, and deeper visibility into CrowdStrike FDR data.

Key benefits include:

* Querying all raw event data received from CrowdStrike FDR using XQL.
* Querying critical modeled and unified EDR data via the `xdr_data` dataset.
* Enriching case and issue investigations with relevant context.
* Grouping issues with issues from other sources to accelerate the scoping process of cases, and to cut investigation time.
* Leveraging the data for analytics-based detection.
* Utilizing the data for rule-based detection, including correlation rules, BIOC, and IOC.
* Leveraging the data within playbooks for case response.

When Cortex XSIAM begins receiving EDR events from CrowdStrike FDR, it automatically creates a new dataset labeled `crowdstrike_fdr_raw`, allowing you to query all CrowdStrike FDR events using XQL. For example XQL queries, refer to the in-app XQL Library.

In addition, Cortex XSIAM parses and maps critical data into the `xdr_data` dataset and XDM data model, enabling unified querying and investigation across all supported EDR vendors' data, and unlocking key benefits like stitching and advanced analytics. While mapped data from all supported EDR vendors, including CrowdStrike, will be available in the `xdr_data` dataset, it's important to note that third-party EDR data present some limitations.

Third-party agents, including CrowdStrike, typically provide less data compared to our native agents, and do not include the same level of optimization for causality analysis and cloud-based analytics. Furthermore, external EDR rate limits and filters might restrict the availability of critical data required for comprehensive analytics. As a result, only a subset of our analytics-based detectors will function with third-party EDR data.

Raw event data from CrowdStrike FDR lacks key contextual information. To enhance its usability, we allocate additional resources to stitch it with other event data and data sources. Therefore, enabling the CrowdStrike FDR integration might temporarily make the tenant unavailable for a maintenance period of up to an hour.

We are continuously enhancing our support and using advanced techniques to enrich missing third-party data, while somehow replicating some proprietary functionalities available with our agents. This approach maximizes value for our customers using third-party EDRs within existing constraints. However, it’s important to recognize that the level of comprehensiveness achieved with our native agents cannot be matched, as much of the logic happens on the agent itself. These capabilities are unique, and are not found in typical SIEMs. Many of them, along with their underlying logic, are patented by Palo Alto Networks. Therefore, they should be regarded as added value beyond standard SIEM functionalities for customers who are not using our agents.

Ensure that your organization has a license for the CrowdStrike Falcon Data Replicator (FDR).

Ensure that CrowdStrike FDR is enabled. CrowdStrike FDR can only be enabled by CrowdStrike Support. If CrowdStrike FDR is not enabled, submit a support ticket through the CrowdStrike support portal.

Follow these steps to check if CrowdStrike FDR is enabled:

1. Log in to the CrowdStrike Falcon user interface using an account that has view/create permission for the API clients and keys page.
2. Navigate to Support → API Clients and Keys.
3. Verify that FDR AWS S3 Credentials and SQS Queue is listed.

* CrowdStrike can provide multiple streams. It can only be read once per stream.
* For more information on configuring data collection from CrowdStrike via Falcon Data Replicator, see CrowdStrike documentation.

### Task 1. Create a CrowdStrike FDR feed

1. In the CrowdStrike user interface, select Support and resources → Resources and Tools → Falcon data replicator.
2. Click the FDR feeds tab.
3. Click Create feed.
4. Enter a feed name.
5. In Falcon Flight Control deployments, there is an option called Select which CID will manage this feed. In typical environments, the parent CID manages the feed for all of its child CIDs. This creates an aggregated feed that has data from all of the child CIDs. For information about aggregated feeds, and how they compare to individual feeds, see CrowdStrike documentation.
   * To set up an aggregated feed, select the parent CID.
   * To set up an individual feed, select a child CID or select both a parent CID and the Exclude Child CIDs option.
   * To exclude only some of the child CIDs, don’t select the Exclude Child CIDs option. Instead, select Customize your FDR feed in the next step.
6. Set the feed status.
7. Select the method for creating your feed, from the following options:
   * Create your FDR feed with default settings, where you get the recommended settings, including all current and future events, all secondary events (if available), and no partitions.
   * Customize your FDR feed, where you start with the option to use a filter to get the specific events that you want in the feed. You can then customize secondary events and partitioning.
8. Include secondary events. They are required for data stitching and enrichment.
9. Optionally, in Flight Control deployments, edit the existing child CIDs included in the feed, and choose whether future CIDs are automatically included, by using the Include future CIDs option.
10. Click Create feed.
11. From the summary page that appears, copy and save all the information shown on the page somewhere safe, for later use. This page includes the credentials that are required for setting up an SQS consumer.

{% hint style="warning" %}
Ensure that you copy the Secret, and store it in a safe place. You will not be able to retrieve it later. If you need a new secret, you must reset the feed credentials.
{% endhint %}

### Task 2. Configure Crowdstrike Falcon Data Replicator

1. Log in to CrowdStrike Falcon using an account that has view/create permission for the API clients and keys page.
2. Navigate to [![cs-logo.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADsAAAAoCAYAAABAZ4KGAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAAB3RJTUUH5QQSDTsWRXPQfwAAA5FJREFUaIHtmSFQKlsYgD/efaOWJThDcRPqjIsFC5u0uCaTG3RMazIxJIu7llcAixpcumDDGSWZWBJp6boUk2yz7ElYeOEODDqKqIBzuXxx55zd/+P8/zn/GUKLi4st/hL++ekARslEdlyZyI4rPWWTyeSo4hgJPWV93yedTr94JsvyUAMaJj1lb25uCIVCL4RlWUbX9aEHNgw+rNlsNsvy8jLn5+dIkoTruiQSiT9S+EPZcDiMYRiEQiHy+TyKomBZFolEovMD/Cn8mp2d/a/XgFgsxsrKCqenp8zPz5PJZAiCgLOzM2ZmZjg5OSEIAjzPG1HIXyfUT29smiZBEJDL5VBVlUwmw+PjI8fHxwDYtk2r1SKXy+E4DkKIoQf+Ffo6Z7PZLOFwmHw+z/39PbquU6/Xub6+RtM0dF3H930ymQzlcpl0Os36+vqwY39BsVikWCz2HPNhGrepVqsIIbBtm2az2VnF3d1dVldXOTg4IBKJEI/HicVibG5uYhgG0WiUcDhMo9Hg+fl5EF5vsr29DcDV1dW7Y/pK424kScI0TVRVxbIsXNfFMAw0TcOyLGzbZmlp6c25juPgOA6lUukznxwYn5Zto6oqyWSSVqvF0dERkiShaRq1Wo2Li4uec4UQFAoFCoXCSOu77zR+TaPRoFQq4fs+pmnSbDapVqs8PDwQiURQFOXdudPT06iqytraGre3t0NN726+fRFwXZe9vT1830fXdYQQZLPZvlZMUZSRNicDu/U4joNt26iqihCCXC7X1zzXdQcVwod8WVaW5U6qSpKELMsIITrBFwqFvjaiQTUjAz16XiOEIB6Ps7+/36nBra0t6vV6J4Vd12VhYYFoNPruezRNY2pqiqenp29tVkM5el4jSRKGYaDrOnNzc8DvJqRSqaAoCo7joOs6mqaRSCR69tKVSgXTNIe2Q39bthtFUdA0jY2NDe7u7ri8vMS2bcrlckdAkqQXO7UQAt/3UVWVVquF4zh91/tnGahsN7IsI8syQRCQz+c/vB05joPneRiGQSqVGsrGNTTZbnRd5/Dw8E3hWq1GqVSi0WgQBAEAhmFgWdbA4/h34G98ByHEC9l2b/3WbjwMURjRysLves5ms52+uX1MeZ43kLaxfezs7Oy8O2ZkK+t5XucC0a7nVCqFJEnEYrGRNBcjW9lu2sfVqC8CPyL7U0z+ERhXJrLjykR2XJnIjit/lez/1yKHlwoJ8FgAAAAASUVORK5CYII=)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/qATr_yEenE8HnjMR5rtXLw-5CAbsl8idaK8R43ZLhoTOw)Support → API Clients and Keys.
3.  On the same line as FDR AWS S3 Credentials and SQS Queue, click Create new credentials.

    CrowdStrike Falcon Data Replicator only supports one FDR credential configuration.
4.  Configure your new FDR credentials.

    [![cs-fdr-credentials-created.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/8G7uHCynn3byKIvwX_GstA-5CAbsl8idaK8R43ZLhoTOw/content?v=7053be22722d53b1\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/8G7uHCynn3byKIvwX_GstA-5CAbsl8idaK8R43ZLhoTOw)
5. Copy the values for the CLIENT ID, SECRET, S3 IDENTIFIER, and SQS URL, and save them somewhere safe, because you will need them when you configure data collection in Cortex XSIAM.

{% hint style="warning" %}
Ensure that you save the SECRET value, because this is the only time that it is displayed. You can go back to this page later to copy the other credentials, but you will not have access to the secret again.
{% endhint %}

6\. Click DONE.<br>

### Task 3. Configure ingesting into Cortex XSIAM

1. Navigate to Settings → Data Sources & Integrations.
2. On the Data Sources & Integrations page, click + Add New, search for CrowdStrike Falcon Data Replicator, then hover over it and click Add.
3. Set these parameters:
   * Name: Specify a descriptive name for your log collection configuration.
   * SQS URL: Specify the SQS URL you received when you created the FDR credential in CrowdStrike Falcon, as explained above.
   * AWS Client ID: Specify the CLIENT ID you received when you created the FDR credential in CrowdStrike Falcon, as explained above.
   * AWS Client Secret: Specify the SECRET you received when you created the FDR credential in CrowdStrike Falcon, as explained above.
4. Click Test to validate access, and then click Enable.

When events start to come in, a green check mark appears below the CrowdStrike Falcon Data Replicator configuration, along with the amount of data received.

<br>
