# Content Pack README

For larger packs that provide at least one end-to-end use case you should create a detailed README file for the pack that is displayed in the **Details** tab of the pack in the Marketplace. The README.md file should be markdown formatted and placed in the **`Packs`** root directory. The file should contain a more detailed overview of the pack compared to the **Description** section. You can add any information you see fit to include about the pack. We recommend providing an overview of what the pack does and how to start working with the pack.

#### README structure

If the pack is a beta pack, add the following at the beginning of the pack README file:

_Note: This is a beta pack, which lets you implement and test pre-release software. Since the pack is beta, it might contain bugs. Updates to the pack during the beta phase might include non-backward compatible features. We appreciate your feedback on the quality and usability of the pack to help us identify issues, fix them, and continually improve._

If the pack is adopted, add the correct text as specified on the [Adopt-a-Pack page](https://xsoar.pan.dev/docs/partners/adopt#text-for-the-pack).

Each pack README should contain:

* A short paragraph connecting real-life situations to the pack use cases.
* A "What does this pack do?" section, explaining point-by-point the capabilities of the pack or the main playbook of the pack.
* (Optional): a sentence or two detailing the contents of the pack.
* When content packs contain multiple playbooks, the content pack README should contain a reference to the README of the main playbook that contains the playbook logic. For example, include: **For more information, visit the Parent Playbook Name documentation**.
* For packs that contains playbooks, a YouTube video is helpful.

![xsiam-content-pack-readme.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-2e530aee2efd3d27549e22ece2e0d14bef362f85%2F964fc876542f218bd8961a15a9b2fd7131ab40cb1c77d5042abcc5d9e4c8642b.png?alt=media)

#### Cortex XSIAM pack README structure

```programlisting
# Product Name
This pack includes Cortex XSIAM content.

## Configuration on Server Side

## Collect Events from Vendor
(Add the options for collections)

### Collection method (Replace with the collection method name)

#### Filebeat Configuration File (if applicable)
```

_`README example`_

````programlisting
# Microsoft DNS

This pack includes Cortex XSIAM content.

## Configuration on Server Side

1. Open the RUN window and enter: dnsmgmt.msc.
2. Right-click the name of the DNS server in the left-hand panel and select **Properties**.
3. In the Debug logging tab, add a check in **Log packets for debugging**
4. Ensure the following are checked: **Outgoing**, **Incoming**, **Queries/Transfers**, **Updates**.
5. For long (detailed) logs, select **Details** and enter the log file path: ```c:\Windows\System32\dns\DNS.log```      

   *Note: Detailed captures will heavily bloat the logs.*

## Collect Events from Vendor

In order to use the collector, use the [XDRC (XDR Collector)](#xdrc-xdr-collector) option.

### XDRC (XDR Collector)

To create or configure the Filebeat collector, use the information described [here](https://docs.paloaltonetworks.com/cortex/cortex-xdr/cortex-xdr-pro-admin/cortex-xdr-collectors/xdr-collector-datasets#id7f0fcd4d-b019-4959-a43a-40b03db8a8b2).

You can configure the vendor and product by replacing [vendor]\_[product]\_raw with *msft_dns_raw*.

When configuring the instance, you should use a YML file that configures the vendor and product, as shown in the below configuration for the Microsoft DNS product.

Copy and paste the following in the *Filebeat Configuration File* section (inside the relevant profile under the *XDR Collectors Profiles*).

#### Filebeat Configuration File

```filebeat.inputs:
  - type: filestream  
    paths:
     - c:\Windows\System32\dns\DNS.log
processors:  
  - add_fields:      
        fields:        
            vendor: msft        
            product: dns
```

**Note**: The above configuration uses the default location of the logs.
````

How the README fie is displayed:

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-b4aad9c8aef2bf5286b2f1bb6a999fb080fe7717%2Ff96f7d4aee17dc93ba496ef7366232396e46e5a40ba6ff568cd487f0eee84316.png?alt=media)

#### Images and Videos

**Images**

Images can provide a useful addition to the pack README.md to help users get a quick understanding of the pack. Images in a content pack README can be included only as absolute URLs.

**Videos**

You can add an image placeholder which links to an external video.

To add an external video hosted on YouTube, use this snippet template (replace \[YOUTUBE\_VIDEO\_ID] with your YouTube video ID):

`[![Video Name](https://img.youtube.com/vi/[YOUTUBE_VIDEO_ID]/0.jpg)](https://www.youtube.com/watch?v=[YOUTUBE_VIDEO_ID] "Video Name")`
