---
description: File structure for files included in the Cortex XSIAM content pack.
---

# Content pack structure

For better separation between content artifacts from different use cases and partners, we use a directory structure called content packs. Each content pack behaves like a mini content repo. It contains all relevant content items within its directory.

For example, the Cortex XDR pack can be seen in the content repository [Packs/CortexXDR](https://github.com/demisto/content/tree/master/Packs/CortexXDR).

To generate a new pack, use [demisto-sdk init --pack](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-guide/demisto-sdk-commands/init)

#### Directories

The directories within the pack represent all the possible content entities. Each pack is located in the Content repo under **`Packs/<Pack Name>`**.

```programlisting
- Integrations
- Scripts
- Playbooks
- Reports
- Dashboards
- IncidentTypes
- IncidentFields
- Layouts
- Classifiers
- IncidatorTypes
- IndicatorFields
- Connections
- TestPlaybooks
- ParsingRules
- ModelingRules
- CorrelationRules
- ReleaseNotes
- Triggers
- XSIAMDashboards
```

#### Pack files

The pack directory contains multiple configuration files used for metadata and documentation.

{% hint style="info" %}
### Note

All ofthe following files are created using the `demisto-sdk init --pack` command, and some of them need to be manually populated.
{% endhint %}

**pack\_metadata.json**

This file contains all the relevant metadata about the pack.

The following fields are populated in the pack metadata.

| Field Name        | Field Type | Field Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name              | String     | The pack name, usually the name of the integration the pack contains (for example Cortex XDR) or the use case implemented in it.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| description       | String     | A short overview of the pack.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| support           | String     | <p>Should be one of the following:</p><p><code>xsoar</code> - Supported by Cortex XSIAM.</p><p><code>partner</code> - Supported by a Cortex XSIAM partner.</p><p><code>developer</code> - Supported by an independent developer/organization.</p><p><code>community</code> - Not officially supported, but available for the community to use.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>For <code>partner</code> and <code>developer</code>, either email address or URL fields must be filled out.</p></div> |
| currentVersion    | String     | The pack version, in the format of x.x.x. For the initial release, this should be set to "1.0.0". See [Content Pack Versioning](#UUID-1c57a2eb-d98f-d6e4-53aa-c4bddde51eae_section-idm4582827879899233663866238317).                                                                                                                                                                                                                                                                                                                                                                      |
| author            | String     | The name of the organization (for partners) or developer (for individual contributions) that developed the integration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| url               | String     | The URL users should refer to for support regarding the pack. Usually, it is the organization support URL or the developer GitHub repository. If left empty the default support site presented to users is the [Live Community](https://live.paloaltonetworks.com/t5/cortex-xsoar-discussions/bd-p/Cortex_XSOAR_Discussions) site.                                                                                                                                                                                                                                                        |
| videos            | String     | The pack Youtube video link.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| email             | String     | The email address users should reach out to for support regarding the pack.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| categories        | List       | The use case categories that are implemented in the pack, usually set by the integration. See the [category list](https://github.com/demisto/content/blob/master/Config/approved_categories.json).                                                                                                                                                                                                                                                                                                                                                                                        |
| tags              | List       | [Tags](https://github.com/demisto/content/blob/master/Config/approved_tags.json) to be attached to the pack in the Marketplace.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| created           | String     | Pack creation time in ISO 8601 format - YYYY-MM-DDTHH:flag\_mm:ssZ. For example 2020-01-25T10:00:00Z.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| useCases          | List       | [Use cases](https://github.com/demisto/content/blob/master/Config/approved_usecases.json) implemented by the pack.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| keywords          | List       | List of strings by which the pack can be found in Marketplace.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| marketplaces      | List       | <p>The Marketplace(s) in which the pack can be found.</p><ul><li>For Cortex XSIAM: marketplacev2</li><li>For Cortex XSOAR 6 and 8: xsoar</li><li>For Cortex XSOAR 6: xsoar_on_prem</li><li>For Cortex XSOAR 8 (Cloud and On-prem): xsoar_saas</li></ul>                                                                                                                                                                                                                                                                                                                                   |
| hidden            | Boolean    | (Optional) Whether to hide the pack from Marketplace. If hidden, updates to this pack will not be published to the Marketplace and the pack cannot be installed.                                                                                                                                                                                                                                                                                                                                                                                                                          |
| dependencies      | Dictionary | (Optional) The content packs that the pack is dependent on. Should be empty on pack creation, as it is calculated by Cortex XSIAM content infrastructure.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| displayedImages   | List       | (Optional) Images to be displayed in Marketplace. Should be empty on pack creation, as it is calculated by Cortex XSIAM content infrastructure.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| githubUser        | List       | (Optional) List of Github usernames to receive notification in the PR in case pack files were modified.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| devEmail          | List       | (Optional) List of emails to receive notification in case contributed pack files were modified.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| certification     | String     | (Optional) If the pack is certified, the value of this field should be `certified`. The possible values are `certified` and `verified`.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| itemPrefix        | String     | (Optional) String to overwrite pack fields prefix. You can specify an alternate string instead of the default pack name enforced by the validation process.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| defaultDataSource | String     | (Optional) Default data source integration in Cortex XSIAM for packs that have more than one fetching integration. We recommend setting the default data source integration to the event collector or the most used integration.                                                                                                                                                                                                                                                                                                                                                          |

<details>

<summary>Pack metadata file contents example</summary>

```programlisting
{
    "name": "Palo Alto Networks Cortex XDR - Investigation and Response",
    "description": "Cortex XDR is the world's first detection and response app that natively integrates network, endpoint and cloud data to stop sophisticated attacks.",
    "support": "xsoar",
    "currentVersion": "1.0.0",
    "author": "Cortex XSOAR",
    "url": "https://www.paloaltonetworks.com/cortex",
    "videos": "https://www.youtube.com/watch?v=ium2969zgn8",
    "email": "",
    "categories": [
        "Endpoint"
    ],
    "tags": [
        "Recommended by Cortex XSOAR",
        "xdr"
    ],
    "created": "2020-03-11T13:16:53Z",
    "useCases": [
        "Malware"
    ],
    "keywords": [
        "adaptive cyber protection",
        "apt"
    ],
    "dependencies": {
        "Base": {
            "mandatory": true,
            "name": "Base"
        },
        "CortexXDR": {
            "mandatory": false,
            "name": "Palo Alto Networks - Cortex XDR"
        }
    },
    "marketplaces": [
        "marketplacev2"
    ],
    "displayedImages": [
        "CortexXDR"
    ]
}
```

</details>

<details>

<summary>Supported Partner pack metadata contents example</summary>

```programlisting
{
    "name": "Product name",
    "description": "Pack description",
    "support": "partner",
    "currentVersion": "1.1.0",
    "author": "Partner name",
    "url": "https://support.<partner>.com",
    "email": "support@<partner>.com",
    "devEmail": "dev@<partner>.com",
    "categories": [
        "Deception"
    ],
    "tags": [],
    "created": "2020-03-19T09:39:30Z",
    "useCases": [],
    "keywords": [],
    "dependencies": {},
    "marketplaces": ["marketplacev2"]
    "githubUser": [
        "<partner Github username>"
    ]    
}
```

</details>

#### Content pack versioning

Pack versions have the format MAJOR.MINOR.REVISION:

`Revision` when you make backward compatible bug fixes.

`Minor` when you add functionality in a backward compatible manner.

`Major` when you make incompatible API changes or revamp the pack by adding significant new backward compatible functionality.

#### README.md

This file contains a general explanation for the pack. You can add any information relevant for the pack. For more details see the [Content Pack README](../documentation/content-pack-readme).

#### .secrets-ignore

This file is used while running [demisto-sdk secrets](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-guide/demisto-sdk-commands/secrets) as an allow list of approved words for the PR.

{% hint style="info" %}
### Note

We use `demisto-sdk secrets` as part of our pre-commit hook to check that possible secrets in the PR aren't exposed to a public repository.
{% endhint %}

#### .pack-ignore

This file allows ignoring linter errors while lint checking and ignoring tests in the test collection.

To add ignored tests/linter errors in a file:

1. Add the file name to the `.pack-ignore` in the format `[file:integration-to-ignore.yml]`
2. On the following line add `ignore= flag`, with one or more comma-separated values:
   * `auto-test` - Ignore the test file in the build test collection.
   * `linter code` - For example, IN126, ignore linter error codes.

By default, script/integration unit tests run without a Docker network.

If one of the integrations/scripts inside a pack needs a network during the unit tests run, use this format:

```programlisting
[tests_require_network]
integration-id-1
script-id-1
```

Example: .pack-ignore

```programlisting
[file:playbook-Special-Test-Not-To-Run-Directly.yml]
ignore=auto-test

[file:integration-to-ignore.yml]
ignore=IN126,PA116

[tests_require_network]
integration-id-1
script-id-1
```

#### Author\_image.png

You can add an author image (logo of the contributing company) which is displayed on the Marketplace page for the content pack, under the the PUBLISHER section. The image should be saved in the root directory of the content pack, for example `content/packs/MyPackName`, and be named `Author_image.png`). Make sure to use this exact file name for the image to appear. The image size should be up to 4 KB and dimensions of 120x50 pixels.

For Partners, this image is mandatory and is validated as part of the build process. If the file is missing, the build fails with the following validationerror:

```programlisting
- Issues with unique files in pack: $PACK_NAME
  Packs/$PACK_NAME/Author_image.png: [IM109] - Partners must provide a non-empty author image under the path Packs/$PACK_NAME/Author_image.png
```

If the file `Author_image.png` does not exist, the name of the author is displayed in the PUBLISHER section instead.

#### CONTRIBUTORS.json

If you are contributing to an existing pack, you can add a CONTRIBUTORS.json file to the root of the pack if one does not already exist. The file should contain a list of strings including your name.

Example: CONTRIBUTORS.json file

```programlisting
[
    "Jane Doe",
    "John Smith"
]
```

Once your contribution is merged, pack details shows the following:

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-8b0885ee7ddd40d3efe58fac41856d99515eaecb%2Fe8077b816e5f3ee7cc875e4bbb0c0d0176be89ae0fa0e12d6671c45ab61506b2.png?alt=media)
