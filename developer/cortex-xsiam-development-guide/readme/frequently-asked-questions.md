---
description: >-
  Cortex XSIAM development FAQs covering IDEs, tools, languages, operating
  systems, licensing, and CLA troubleshooting.
---

# Frequently asked questions

<details>

<summary>Which IDE should I use?</summary>

When it comes to an external IDE, you have multiple options. .

Cortex XSIAM offers a free [Visual Studio Code extension](content-development-environments/visual-studio-code-extension) that simplifies/automates tasks such as:

* Running unit tests
* Creating a blank integration or automation script
* Uploading/downloading your integration code to/from Cortex XSIAM

However, if you want to use a different IDE (for example Sublime, vi, emacs), some tasks must be performed manually. To automate them, you can use the [Demisto SDK](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/README).

You can also write code directly in the Cortex XSIAM, but is not recommended if you want to contribute supported content. Check [here]() for details.

{% hint style="info" %}
### Note

IDEs are used only for writing integrations and scripts, everything else (for example playbooks, dashboards, and layouts) should be developed in the Cortex XSIAM UI.

Once the resource is developed in the Cortex XSIAM UI, you can download it using `demisto-sdk download -i "$NAME_OF_RESOURCE"` or export it from the UI.
{% endhint %}

</details>

<details>

<summary>Which software development tools should I use?</summary>

While the basics of writing code and changing configuration options can be done in the Cortex XSIAM UI, for complex solutions and supported contributions you'll probably need a combination of both the Cortex XSIAM UI and other tools. See [Content development environments](content-development-environments) for more information.

We recommend using Visual Studio Code with the Cortex XSOAR extension when you want to contribute content to the Marketplace. The Cortex XSOAR extension works with both Cortex XSOAR and Cortex XSIAM.

We recommend using the Cortex XSIAM UI when:

* Creating [Playbooks](../playbooks).
* Creating non-code entities (everything but integrations and scripts), such as:
  * Alert fields, types and layouts
  * Indicator fields, types and layouts
  * Classifiers and mappers
  * Widgets
  * Dashboards
* Working on the properties of your integration/script (parameters, commands, arguments, and outputs) in the [YAML](../integrations-and-scripts/components/integration-metadata-yaml-file) file - this can also be done using [Visual Studio Code extension](content-development-environments/visual-studio-code-extension).
* Testing the user experience for what you developed.

</details>

<details>

<summary>What programming languages do you support for integrations and scripts?</summary>

*   Python

    Python is the preferred development language, since it provides a wider set of capabilities and tools. Cortex XSIAM supports Python 3, and new contributions must be developed in Python 3.7 or later.
*   PowerShell

    Cortex XSIAM supports PowerShell integrations and scripts.

</details>

<details>

<summary>Which operating systems are supported for development?</summary>

The recommended OS for development is either macOS or Linux, as Bash and Docker are used in some validation/testing flows.

For Windows, you can either work with a Linux VM or use [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install).

</details>

<details>

<summary>What license applies to the Cortex XSIAM content repository?</summary>

The Cortex XSIAM content repository has an [MIT License](https://github.com/demisto/content/blob/master/LICENSE).

</details>

<details>

<summary>Why is my CLA pending after I signed the agreement?</summary>

The CLA should be signed by all branch committers. The CLA bot will let you know the committers who have not yet signed the agreement by marking them with a red X.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-98d17fcb0f7d72c0cdbf4992d64e975db914fa08%2Fd1ab12bc87bbe24b8e84e6389b0c7f8ee2faea724646efe62626a79ffc337b63.png?alt=media)

If the missing user appears under one of your commits (can be checked by visiting the **Commits** tab in the PR), it probably means that one of your commits was done with this user. Try the following:

1. If you have the credentials for the missing user, try to log in and sign the CLA, then click the **recheck** button at the bottom of the CLA message.
2. Try to link your commits: Add the email address of the missing user to your GitHub email settings, then click the **recheck** button at the bottom of the CLA message.
3. If the missing user is not a real user or named `Root`, you need to open a new branch:
   1. In your local environment, manually copy the code you edited (usually you can copy the entire pack) to another location.
   2. Check out the master branch.
   3. Create a new branch.
   4. Paste the code from before into your new branch.
   5. Commit and push your new branch.
   6. Open a new Pull Request for the new branch.
4.  If the license/CLA status check remains on **Pending** even though all contributors have accepted the CLA, you can recheck the CLA status by visiting the following link (replace `[PRID]` with your PR ID):

    [https://cla-assistant.io/check/demisto/content?pullRequest=\[PRID\]](https://cla-assistant.io/check/demisto/content?pullRequest=%5BPRID%5D%20)

{% hint style="info" %}
### Important

Don't forget to close the old PR and delete the old branch.
{% endhint %}

You can find information about troubleshooting commits in the GitHub docs site [Troubleshooting Guide](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/troubleshooting-commits/why-are-my-commits-linked-to-the-wrong-user).

</details>
