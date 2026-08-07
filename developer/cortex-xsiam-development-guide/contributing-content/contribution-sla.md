---
description: >-
  An SLA detailing the required services and the expected level of services when
  contributing content to the Cortex XSIAM Marketplace
---

# Contribution SLA

You can contribute content to the Cortex XSIAM Marketplace by contributing through a GitHub pull request on the public [content repository](https://github.com/demisto/content). For more information, see [Contributing content]().

A review phase begins with the opening of the GitHub pull request containing your changes or new content.

#### Cortex XSIAM content team commitments

Once your PR is open, the content team commits to the following time frames:

1. After the PR is opened, a reviewer is assigned to your PR and publishes the initial response to your submission within five business days.
2. If you are asked to make changes, you need to make those changes, and add a corresponding message in the pull request. Your reviewer responds within three business days. You might have multiple rounds of fixes. These commitments are the same for each round.
3. Your reviewer is available for any questions during the review process. You can contact your reviewer via the PR itself or on Slack ([DFIR Slack Community](https://start.paloaltonetworks.com/join-our-slack-community)).
4. Once your PR is approved and merged by your reviewer, an internal PR including your changes is opened within an hour. The internal PR allows us to run our internal validity and security checks on your final code. The internal PR is merged within three business days. If during the internal PR phase we discover issues related to the code changes made in the contribution, the contributor may be asked to help resolve them.
5. Once the internal PR is merged, your changes are published in the Marketplace within three business days.

#### Contributor commitments

The content team requires contributors to:

* Provide the content team with as much information as possible about changes made or about new content you have created. Provide this information in the pull request body by filling in the template.
*   Register your contribution by filling out the contribution registration form, and sign the [CLA](https://github.com/demisto/content/blob/master/docs/cla.pdf) (Contributor License Agreement). The review process does not start until those forms are completed.

    Links to the Contribution registration form and to the CLA appear on your PR:

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-413c74862d0be0734d01ae26a845ed3a4716adb7%2F56b08acbbf5c13942cc1c2121ca2c71bc73228d1224b95f2fe0cc59d5d6741c5.png?alt=media)

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-67c97a18d46119f157cea93d14449840a83f99d6%2F2dd1da7c225e943a4a694fffb0ae56e50ddebbbc89aa9fc57e8cc6e513a14e60.png?alt=media)
* Provide the content team with a [recorded demo session](contribution-demo-preparation) that demonstrates your changes. Add the link to the contribution registration form.
* Check the status of the build of your PR once it is completed. If the build includes errors, try to solve them. For more information, see [the build process](pull-request-conventions).
*   During the review process, monitor your PR. Your reviewer may add comments to the PR, asking questions and requesting changes. To expedite the review process for your contribution, respond to the reviewer's code review and apply the required changes within 14 days. Stale pull requests can be closed.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Once your pull request is reviewed, only add or update content items that were requested during the review process. If you have new content items to add, open a new pull request. If you are not sure whether to open a new pull request, consult the reviewer.</p></div>
* If your contribution includes changes in an Cortex XSIAM supported content pack, you must conform to the Cortex XSIAM code and documentation standards, and add unit tests and a test-playbook to test your code. For more information see [Python code conventions](../integrations-and-scripts/developing/python-code-conventions), [Documentation](../documentation), [Unit testing](../testing/unit-testing), and [Test playbooks](../testing/test-playbooks).

While the content team tries to merge and publish your changes as quickly as possible, the duration of the review process depends on many factors including the level of support of the edited content pack, the number and complexity of changes, and various validations and security tests.
