# Cloud causality view

On the cloud causality view you can analyze and respond to Cortex XSIAM issues and cloud audit logs. On this view you can see the causality (cause and effect) of events of the entire process execution chain that led up to the issue. The cloud causality view presents the event identity and /or IP address and the actions performed by the identity on the cloud resource. On each node in the CI chain, Cortex XSIAM provides information to help you understand what happened around the event.

The following sections describe the different areas of the cloud causality view:

<details>

<summary>Causality instance chain</summary>

Includes the graphical representation of the Causality Instance (CI) along with other information and capabilities to enable you to conduct your analysis.

The view presents a single event CI chain. The CI chain is built from Identity and Resource nodes. The Identity node represents for example keys, service accounts, and users, while the Resource node represents for example network interfaces, storage buckets, or disks. When available, the chain might also include an IP address and issue that were triggered on the Identity and Cloud Resource.

Causality data is displayed as follows:

* **Identity node:** Displays the name of the identity, generated issue information, and if available the associated IP address.
* **IP address node:** Displays the IP address associated with the Identity.
* **Operations:** Lists the type of operations performed by the identity on the cloud resources. Hover over the operation to display the original operation name as provided by the cloud Provider.
* **Cloud resource node:** Displays the referenced resource on which the operation was performed. For more information about cloud resource icons, see **Key of cloud resource icons** below.

#### **Navigation**

You can move the chain, extend it, and modify it. To adjust the appearance of the CI chain, use the size controls on the right. You can also move the chain by selecting and dragging it. To return the chain to its original position and size, click <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-02413f496b1c767ec7cb02225bc1e0e6c8b66b8b%2Fdb69f0a560c666334cf243831344778fcda2e5341654ae3631d61bc10b019357.png?alt=media" alt="causality-view-reset-icon.png" data-size="line"> in the lower-right of the CI graph.

#### To further investigate the user

1. Hover over an Identity node to display, if available, the identity Analytics Profiles.
2. Select the Identity node to display in the Entity Data section additional information about the Identity entity.
3. Select the issue icon to display additional information in the Forensic Highlights section.

#### To further investigate the resource

1. Hover over a resource node to display, if available, the resource Analytics Profiles and Resource Editors statistics.
2. Select the resource node to display in the Entity Data section additional information about the resource entity.

</details>

<details>

<summary>Information Overview</summary>

Summarizes information about the issue you are analyzing, including the type of Cloud Provider, Project, and Region on which the event occurred. Select **View Raw Log** to view the raw log as provided by the Cloud Provider in JSON format.

</details>

<details>

<summary>All Events table</summary>

Displays up to 100,000 related events and up to 1,000 related issues. In the **All Events** table, Cortex XSIAM displays detailed information about each of the related events. To simplify your investigation, Cortex XSIAM scans your Cortex XSIAM data aggregating the events that have the same Identity or Resource and displays the entry with an <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a2f001ce9456c1424ca2b48c506a1e02056763f3%2F862436a5df1eb6af965121c50352fb99efa8bc5af597dd078606e6db8cd7a573.png?alt=media" alt="cloud-causality-aggregated-events.png" data-size="line"> aggregated icon. Right-click and select **Show Grouped Events** to view the aggregated entries.

Entries highlighted in red indicate that the specific event created an issue. To continue the investigation, right-click to **View in XQL**. To continue the investigation, in the **Issues** table, right-click an issue to see the available actions.

</details>

<details>

<summary>Key of cloud resource icons</summary>

The following table lists the cloud resource icons:

| Icon                                                                                                                                                                                                                                                                                                 | Type of Resource                     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| ![cloud-causality-compute-instance.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ed5ff932d700030c58d13a7842f4f6bc96e25a28%2Fc35464002303e76eb0f8767133fa606adeb67eeb142b0d83ad6485c76cf34366.png?alt=media)  | Compute instance resource            |
| ![cloud-causality-disks.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-5627217adf30a9e9af469b68754f4d352ef77cd1%2F156f0f31ec878cd0e78b5a1ef7683fe4a389bbc0450bd3330198e5f3491520f4.png?alt=media)             | Disk resource                        |
| ![cloud-causality-general.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-1ddcbcb09b98cab3778c1d793285444c2b21e06a%2Ff386acbf70f205698c12d4f4c4b723df91fc8f06573e5d0c32800450e20e9b7f.png?alt=media)           | General resource                     |
| ![cloud-causality-images.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-a5a32d44cdf148d42acb5dc79a512daf5e5b4e58%2Fe129d6716ed7509103f91513d508f1c581cf3e1c26885ddbe146926acf47e68b.png?alt=media)            | Image resource                       |
| ![cloud-causality-network-interface.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-eec8deebc71a7b057a7c286e5ceb71e94b5eac8a%2F4b59c9bcb53771f1da3f14e39f0bd884a7c1e8b6cb6ab30458d642200de655d9.png?alt=media) | Network interface resource           |
| ![cloud-causality-fw.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-67afc047d53c3efe7cf3615160dd5c469dca9711%2Fbf518c31f50c2fb576fa3803e1b21701e3fd06f833a5f25f5d279c0c0cfeeda0.png?alt=media)                | Security group (FW rule) resource    |
| ![cloud-causality-bucket.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-41c0ebc67705889faaa8f76d9d215271aa37f4e0%2F3f1f37a78b489c4617be1891d9db81ea795a6dacc2e8e3422f7441f9ec8f49f0.png?alt=media)            | Storage bucket resource              |
| ![cloud-causality-vpc.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-26e2b8df55fd79d6417c89f2404c98a6e56e4209%2Fb1340b413b02ea6a2e1ccf90efb8c9c2c92a52e931dc8c9c9ff2e08223807f4e.png?alt=media)               | Virtual private cloud (VPC) resource |

</details>
