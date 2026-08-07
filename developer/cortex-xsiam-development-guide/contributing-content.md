---
description: How to contribute content for Cortex XSIAM.
---

# Contributing content

Contributing enables clients and partners who create new content, or who modify existing content (enhancements, bug fixes, etc.) to share their work with the community by making it publicly available in the [Marketplace](https://xsoar.pan.dev/marketplace). Content can be Cortex XSIAM, partner, or community supported.

If you are beginning development, we recommend you first review [Getting started](readme). If you have questions or need support with the development or contribution process, contact us via the [#demisto-developers](https://start.paloaltonetworks.com/join-our-slack-community) slack channel.

{% hint style="info" %}
### Note

This topic is only related to Cortex XSIAM content. For documentation contributions, see [Documentation Contributions](documentation/documentation-contributions).
{% endhint %}

All content is open source and resides in the Cortex XSIAM GitHub Repository, with a MIT license.

### Support and Requirements

Contributions can be either officially supported (by Palo Alto Networks or a Technology Partner), or community supported. Officially supported content packs have a stricter quality-control process and provide an email address or website for support. Community supported content packs do not have a support contact. Customers can ask questions about community supported packs on the [Live Community](https://live.paloaltonetworks.com/t5/cortex-xsoar-discussions/bd-p/Cortex_XSOAR_Discussions)

{% hint style="info" %}
### Note

If you contribute content that integrates with one of Palo Alto Networks' products, we require the pack to be supported by Cortex XSIAM. Due to this support requirement, in some cases we may adopt your pack and push it into the Cortex XSIAM development pipeline to be released as Cortex XSIAM supported.
{% endhint %}

For more information about the different support levels, see the [support types](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/) documentation.

### How to Contribute

Before you begin contributing content, we recommend reviewing the [Contribution SLA](contributing-content/contribution-sla), which details the requirements for content contributions. After you have created your content, you must submit your content to Palo Alto Networks for review. The Cortex XSIAM content team reviews and approves all content before it becomes available to customers.

To submit your content:

*   Contribute through a GitHub pull request on the public Cortex XSIAM content repository. We recommend using this workflow in the following scenarios:

    * You are a Technology Partner contributing partner supported new content.
    * Your contribution is large and contains many different parts (integrations, scripts, playbooks, layouts, etc.) and is likely to lead to a complex review process.
    * You are proficient with GitHub.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>We recommend using a GitHub Codespace, which provides you with a pre-configured ready-to-use development environment. This method is still experimental, but makes the contribution, development, and review processes easier. For more information and a step-by-step guide, see <a href="readme/content-development-environments/set-up-a-github-codespace-environment">Set up a GitHub Codespace environment</a>.</p></div>

This document describes the main workflow for supported and community contributions, and summarizes everything you must do before and after opening a pull request on GitHub to contribute your pack. These steps are not required if you are contributing community supported content, but we recommend reviewing this document to be aware of best practices.

### Contributor Guidelines

Please read the following guidelines carefully. Following these guidelines will provide for a fast, easy, and effective review process for everyone involved. If anything is unclear, please reach out to us via [Slack](https://start.paloaltonetworks.com/join-our-slack-community) on the #demisto-developers channel.

1. Start by designing your contribution. Follow the [design](readme/design) guidelines to identify exactly what you want to build and to verify it's aligned with our [best practices](readme/design/design-best-practices).
2. Verify that you have met all the [requirements for contributions](contributing-content/contribution-requirements).
3. [Set up a development environment](readme/content-development-environments/set-up-a-local-development-environment), a preconfigured [GitHub Codespace environment](readme/content-development-environments/set-up-a-github-codespace-environment), or a [containerized development environment](readme/content-development-environments/set-up-a-containerized-development-environment).
4. Follow the [content pack structure](contributing-content/content-pack-structure) to build your contribution. Use [demisto-sdk init](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/init) to help create it.
5. If you are updating an existing content pack, verify it is updated with the latest version available in the Marketplace before proceeding.
6. Depending on the content entities you need to build, navigate to the specific sections of this website for more details. If you are creating integrations and/or scripts), verify that you:
   * Use the proper [integrations/scripts directory structure](integrations-and-scripts/components/integration-directory-structure). Use [demisto-sdk init](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/init) to help create it. If working on existing code, beyond minor changes, convert to this structure as it allows you to run linting and unit tests and provides a clearer review process.
   * Understand the structure of the [YAML file](integrations-and-scripts/components/integration-metadata-yaml-file) and the [parameter types](integrations-and-scripts/components/integration-and-script-parameter-types).
   * Verify your integration follows our [logo guidelines](integrations-and-scripts/components/integration-logo-requirements).
   * Read and follow [Python code conventions](integrations-and-scripts/developing/python-code-conventions) (recommended) or [Powershell code conventions](integrations-and-scripts/developing/powershell).
   * Verify your commands make proper use of the [context](integrations-and-scripts/developing/context-and-outputs), including [context standards](integrations-and-scripts/developing/context-standards) and [DBotScore](integrations-and-scripts/developing/reputation-and-dbot-score).
   * Create [unit tests](testing/unit-testing) and verify the various linters we support pass as detailed [here](testing/linting).
   * Document your integration or script by generating the [README files for content entities](documentation/readme-files-for-content-entities).
7. Create the appropriate [content pack documentation](documentation/content-pack-metadata-file).
8. Follow the [documentation best practices](documentation/documentation-best-practices).
9. As you build newer versions of your content pack, document your changes in relevant [release notes files](documentation/content-pack-release-notes).

After completing these steps, you should be ready to submit a pull request.

A working example that summarizes all of the above is the [Hello World content pack](https://github.com/demisto/content/tree/master/Packs/HelloWorld) that you can use as a reference. We also recommend reviewing the [Hello World Design Document](https://github.com/demisto/content-docs/files/14121809/Cortex.XSOAR.Content.Pack.Design.Document.-.Hello.World.V1.pdf).

### Pull requests

#### Before opening a pull request

To submit a pull request to the Cortex XSIAM [GitHub repository](https://github.com/demisto/content), you need to:

* Review the [file checklist](contributing-content/file-checklist) to verify you have included all necessary files.
*   Verify you are working on a GitHub fork of the Cortex XSIAM content repository, and create a branch for your contribution. Do NOT submit changes to the master branch.

    ![content-new-fork.gif](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-5782cbe2974b2fc44c8181627f4ba0d8eb720716%2F4dc1d2ed3436678156f9bc7bc67df0267e2c878844d31744a8d5429682cab448.gif?alt=media)
* Validate your content. The validation hook runs automatically every time you run `git commit`. You can also run the validation manually by using [demisto-sdk validate](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-commands/validate). Example: `demisto-sdk validate -i Packs/YourPackName`. If you get an error that is unclear, ask for help on the #demisto-developers channel on our [Slack DFIR Community](https://www.demisto.com/community/).
* If your contribution has integrations or scripts, verify it passes lint checks and unit tests with `demisto-sdk pre-commit -i Packs/YourPackName`.
* Create a short video to demo your product and your pack, and provide the link to the video. The video is used by our reviewers to understand what your product does and how the content pack works.

#### Open a pull request

After you have completed all of the above the requirements and are ready to open your pull request, commit and push your work to the branch you have created in your forked repository. After you push your changes to the remote branch on GitHub, GitHub automatically detects the changes and a green **Compare & pull request** button appears at the top.

![compare\_and\_pull.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-d21ec60a6fbb02367c7976dcffdc62e21a91f251%2Fcb22ce66c42f33b011dd2a1bac138b8a4b97fad0747ee1c87abb6401b402a1e8.png?alt=media)

Click **Compare & pull request**. When the form opens, update the title and the description, using the pre-existing template, and **Create pull request**.

For more information about creating a pull request from a fork, see the [GitHub documentation](https://help.github.com/articles/creating-a-pull-request-from-a-fork).

{% hint style="info" %}
### Note

By default, the pull request is opened from your fork on the branch you created, to the master branch of the base Cortex XSIAM content repository. After a few minutes, the target branch (master) is replaced with a different custom branch. This is intentional and should not be changed.
{% endhint %}

#### After opening a pull request

* Sign the [CLA](https://github.com/demisto/content/blob/master/docs/cla.pdf). Every contributor must sign our Contributor License Agreement in order for their contribution to be added to our content. If there are CLA issues, see the [FAQ](readme/frequently-asked-questions).
* Fill out the [registration form](https://docs.google.com/forms/d/e/1FAIpQLSd0V270r75tTy9YbT50irQBUpKK8Wfn1aCUihYNn2rc_LkPpA/viewform).
* A contributions team member will begin reviewing your contribution.
* Monitor your pull request on GitHub. Our content team adds comments to the pull request, asking questions and requesting changes as needed. To proceed with your contribution, you are asked to respond to the reviewer's code review and apply the required changes within 14 days. Stale pull requests may be closed.
* We may contact you to schedule an interactive demo. You will need a working instance of Cortex XSIAM with your pack fully configured and ready for presentation. Check out our [contribution demo page](contributing-content/contribution-demo-preparation) for more details.

{% hint style="info" %}
### Note

As part of the pull request template, you are asked to fill in the contribution registration form. The form must be completed for us to review your contribution.
{% endhint %}

For more information about pull requests, see [Pull request conventions](contributing-content/pull-request-conventions).
