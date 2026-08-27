---
description: Cortex XSIAM guidance for README files for content entities.
---

# README files for content entities

Documentation is a critical step that assists customers who may use your integration/script/playbook by providing insight into how the content entity is supposed to work. From creating custom playbooks, to providing background information to assist in debugging, it is important to ensure that the documentation explains every aspect of the integration. Documentation is maintained as `README.md` per integration/script/playbook and made available for customers as part of the [reference docs](https://xsoar.pan.dev/docs/reference/index) of the Cortex XSIAM Developer Hub.

We recommend reviewing the [HelloWorld integration README file](https://github.com/demisto/content/blob/master/Packs/HelloWorld/Integrations/HelloWorld/README.md) as you create the README files for your content entities.

{% hint style="info" %}
**Note**

[Images](images-in-documentation) and [videos](videos-in-documentation) can be added to documentation.
{% endhint %}

### Generate README documentation for content entities

* If the content entity is new.
* If the content entity exists but is missing documentation.
* If the content entity exists and some of it has changed. For example, a new command was added or context was changed.

### Content entity README examples

* [Azure Sentinel](https://github.com/demisto/content/blob/master/Packs/AzureSentinel/Integrations/AzureSentinel/README.md): Shows how the commands and examples should be presented.
* [Slack v2](https://github.com/demisto/content/blob/master/Packs/Slack/Integrations/Slack/README.md): Shows an example of the troubleshooting section.
* [Get Email From Email Gateway - Mimecast](https://github.com/demisto/content/blob/master/Packs/Mimecast/Playbooks/playbook-Get_Email_From_Email_Gateway_-_Mimecast_README.md): show an embedded playbook image.
* [JSON Feed](https://github.com/demisto/content/blob/master/Packs/FeedJSON/Integrations/FeedJSON/README.md): Shows use of embedding a video.
* [CentrifyVault](https://github.com/demisto/content/blob/master/Packs/CentrifyVault/Integrations/CentrifyVault/README.md): Shows use of embedding a YouTube video.

### Publish content entity README documentation

After the pull request with the documentation README file is merged into `master`, it becomes available as part of the Developer Hub, and can be viewed in the [reference docs](https://xsoar.pan.dev/docs/reference/index) section. The site is updated with the latest content on a daily basis. If you wish to preview how the documentation looks at the Developer Hub, before merging to `master`, you can either run locally the content-docs project to preview the Reference Docs site locally or create a PR at the [content-docs repo](https://github.com/demisto/content-docs).

### Preview content entity reference docs locally

Clone or download the [content-docs repo](https://github.com/demisto/content-docs). Follow the instructions at the project's [README](https://github.com/demisto/content-docs/blob/master/README.md) to run the site locally and generate Reference Docs for the content repo you have locally. For example run in the content-docs checkout dir:

```programlisting
CONTENT_REPO_DIR=~/dev/demisto/content npm run reference-docs && npm start
```

### Preview reference docs with a content-docs pull request

Create a PR at the [content-docs repo](https://github.com/demisto/content-docs) with the same branch name as the PR you are working on in the [content repo](https://github.com/demisto/content-docs). Mention in the PR that it is related to a PR from the content repo. Your PR in the content-docs repo will include a preview link in the GitHub Checks section from deploy/netlify. You can perform a dummy white space change for the PR that will re-trigger the build and create a new preview. Example screenshot for preview link:

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-0d9bb9ccc725ab7069e3325702c525eac7011ec0%2Fc4d2d6fce2e390a047caac64d479705a45fa2a5b0d9cba22b82ccb1f911f1726.png?alt=media)

### Use MDX in content entity README files

We use [MDX](https://mdxjs.com/) for the Markdown generation. MDX is a superset of standard Markdown, but it requires that any HTML used in the document must be JSX compliant. This means all HTML tags need to contain a closing tag. For example don't use `<br>`, use `<br/>`. Additionally, HTML entities < >, not in code blocks need to be HTML encoded. Use `&lt;` and `&gt;` to encode. As part of the build, the README.md file is validated for MDX compliance.
