---
description: Cortex XSIAM pull request conventions and build process guidance.
---

# Pull request conventions

If you open a GitHub pull request (PR) against the Cortex XSIAM repository, a reviewer from the content team is assigned to the PR and accompanies you through the process of releasing your contribution.

We recommend you check the PR updates often. If you think the process has stalled, feel free to "ping" the assigned reviewer by adding a new comment to the PR with a [mention](https://github.blog/2011-03-23-mention-somebody-they-re-notified/) or reach out in the #demisto-developers channel in our [Slack Community](https://dfircommunity.slack.com/).

We value your contributions. By following our best practices for pull requests, you can help expedite the contribution process.

### Pull request best practices

Use the following guidelines when working on changes requested by our reviewers.

* Always create PRs from your own fork using a dedicated branch. Do NOT use the `master/main` branch.
* Use clear and brief messages for your commits. See this [article](https://cbea.ms/git-commit/) for good examples.
* Do NOT use force pushes, for example: `git push --force`). If you need to force push, contact us first via the pull request or Slack.
* During the process our reviewers might ask for multiple changes. Work through the entire list and commit all the changes.
* When you push changes to your fork's branch that was used to open the PR, the PR is automatically updated, you don't need to open a new PR. Do NOT open a new PR unless absolutely necessary (i.e. unless asked by the reviewer), as it will make it hard for the reviewer to track their comments.
*   The review usually has a summary and several conversations: make sure you address all the comments, including the ones in the summary:

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-ddabcabbf84c888a389f7c22d6823ae24714f7f4%2Fccd981963b454b560925420e279dcbbfa065a8e95f52596b4f70709b0ababb35.png?alt=media)
*   When addressing the review's conversations, do NOT mark them as resolved. Write `done` in a comment, so the reviewer can keep track of them.

    ![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-7f43f94f8ff9d21fefa5cdea358d0a52328fb586%2F80a235fa6aef843dbb4f6c892fe10e4c3a85c9733e4a0c5fa7b3a0dd6c61cdb2.png?alt=media)
* Once you have pushed all requested changes, please ask for a new review by navigating to Reviewers section in the right sidebar in GitHub and click the ![xsiam-icon.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-82b06de4ab0066adaaf87a8c239875fa3cc9b369%2Fc25d73ad0bd55c27681edbee4be27c05ff3b35456622cabec98b8f1d6781960e.png?alt=media) icon next to the reviewer's name.
*   If the branch you'll be using as the basis for the pull request includes more than 50 commits, squash all commits into a single commit before creating the pull request. This makes the git history cleaner and easier for reviewers. Below is an example of a squash merge after consolidating 122 commits into one:

    ```programlisting
    COMMITS=122

    git reset --hard HEAD~$COMMITS

    git merge --squash HEAD@{1}

    git commit -m "squash last $COMMITS into one"
    ```

    Alternatively, you can use a specific commit to squash from:

    ```programlisting
    COMMIT_HASH=0d1ddfc42

    git reset --hard $COMMIT_HASH

    git merge --squash HEAD@{1}

    git commit -m "squash from $COMMIT_HASH into one"
    ```

### The build process

The commit hooks of the repository automatically run several commands locally on your system, such as [demisto-sdk validate](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-guide/demisto-sdk-commands/validate), that verify your content is valid before you commit and push the changes to your pull request.

There are also jobs that run automatically on your pull request after every push that validate the changes and run the same tests to verify the contribution can be merged and become part of the content. You see several GitHub Status Checks that help validate that your pull request is according to our standards.

After you push changes, go back to the pull request and check the status of the build after it's completed. Pay special attention to the checks for unit testing and validations.

If the error is unclear or you are in doubt, add a comment to the PR to ask the reviewer or post a question in the #demisto-developers channel on [Slack](https://dfircommunity.slack.com/).
