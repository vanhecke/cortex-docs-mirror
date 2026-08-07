---
description: >-
  Information about the pack_metadata.json used to display a description of the
  content pack in the Marketplace, and apply tags, use cases and categories to a
  content pack.
---

# Content pack metadata file

Each content pack contains a `pack_metadata.json` file that contains a short description of the content pack that is displayed in Marketplace. The metadata file also contains tags, categories, and use cases for the content pack.

When displayed in Marketplace, content packs contain the following documentation sections:

*   **Description**: Displayed in the content pack card when browsing Marketplace and at the top of the **Details** tab.

    Example: Content pack card

    ![xsiam-content-pack-description-card.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-fca5a386db500edb835859878f981ac591187be4%2F4709bbe07180456aafa575e3364e0aec4f936eb2e22fa3ea375e7fac8177029a.png?alt=media)

    Example: **Details** tab with Description and README

    ![xsiam-content-pack-description-and-readme.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-aea57edbcace1a4a8b8784f8a437176f2edbe7e8%2F1394fef6aebb542b8be27a544f0a220dbb67753a6cacf3b58987d6724974f238.png?alt=media)
* **Videos**: Displayed in the main display area and in the middle of the **Details** tab.
* **README**: The content pack README file, if it exists, is displayed in the main display area and in the bottom of the **Details** tab.

#### Pack description

The pack description is the first information users see when they go to your content pack. It's important to give a detailed, thorough description of what the pack contains, use cases, and overall benefits of the pack. The pack description is maintained in the pack\_metadata.json file under the description field. Packs should always contain a description, even if a README file is provided with more details. This enables users to get a short overview of the pack when browsing the Marketplace.

**General description guidelines**

* Short and to the point
* Convey gain/benefit for the user
* If possible - what is unique about this pack (for example, minimal, extended, fast, thorough, streamlined)
* Use active voice (you, yours, do, use, investigate) where possible
* Omit redundancy (do not repeat the name of the pack, do not start with "Use this…")
* Capitalize product names
* Use present tense consistently (for example, if "engages" than "investigates", not "investigating")
* Up to 150 chars
* Up to 4 lines

| Examples                                                  | Before                                                                                                                                                                                                                                                                                                                                         | After                                                                                                                                                                         |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Turn a "fat" description into a "lean" description        | <p>300 chars / 44 words</p><p>Use this content pack to investigate and remediate a potential phishing incident. The playbook simultaneously engages with the user that triggered the incident, while investigating the incident itself and enriching the relevant IOCs. The final remediation tasks are always decided by a human analyst.</p> | <p>139 chars / 10 words</p><p>Streamline investigation and remediation of Phishing incidents. Playbook engages with users while simultaneously investigates and enriches.</p> |
| Turn a "passive" description into a "active" description: | <p>Passive and impersonal</p><p>Provides data enrichment for domains and IP addresses.</p>                                                                                                                                                                                                                                                     | <p>Active and personal</p><p>Enrichment for your domains and IP addresses.</p>                                                                                                |

Example sentences:

* "Streamline your \_\_\_ process for \_\_\_. Optimized for \_ and \_\_\_\_ this \_\_\_ targeted content pack is ideal for \_"
* "Eliminate \_\_\_\_ by improving your\_\_. Rich with layouts and playbooks, this content pack is right for \_\_\_\_"
* "Get smarter. This pack utilizes \_ and \_\_\_for when \_ is heavily needed"

#### Pack Videos

For larger packs that provide at least one end-to-end use case, you are encouraged to create a short video or a few videos for the pack that are displayed in the **Details** tab of the pack in Marketplace. The videos files should be hosted on YouTube, and they should contain a more detailed overview of the pack compared to the **Description** section.

Add the video link to the pack\_metadata.json file. For example, for the Malware Investigation and Response content pack:

```programlisting
{
    "name": "Malware Investigation and Response",
    "description": "Accelerate the investigation of your endpoint malware alerts and incidents and trigger containment activities quickly.",
    "support": "xsoar",
    "videos": [
        "https://www.youtube.com/watch?v=DtGIefyoTao"
    ],
```

#### Pack keywords, tags, use cases, and categories

To classify packs and make them easier to find, you can use the following pack metadata elements in the pack metadata file.

![xsiam-pack-metadata.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-8dd8a02e7a768aa935267bd18c4895fb384dcd47%2F40945d73038cc833dccf5b1c5831eec406c98c004632b96f1d88f793e70fe523.png?alt=media)

**Use cases**

The use case must be one or more of the [approved use cases.](https://github.com/demisto/content/blob/master/Config/approved_usecases.json)

**Tags**

Tags make it easier to find packs using filters or the search bar, and are visible on the screen to help understand what the pack is and its benefit to users.

Tags must be from the[list of approved tags](https://github.com/demisto/content/blob/master/Config/approved_tags.json).

**Categories**

The high level field/subject the pack relates to. Your pack should fall into one of the [approved existing categories](https://github.com/demisto/content/blob/master/Config/approved_categories.json).

**Keywords**

Keywords operate like tags to assist in searching for packs, but they aren't displayed in the UI. You can add keywords as needed.

For example, for a pack related to messaging, you may want to add "msg" as a keyword so when a user searches for "msg" they will find the pack, but the word "msg" won't display in the UI.

You can add any keywords you want, the list is not restricted.
