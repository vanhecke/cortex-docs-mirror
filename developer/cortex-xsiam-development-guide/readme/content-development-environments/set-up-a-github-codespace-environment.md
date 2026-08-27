---
description: >-
  Steps for setting up a GitHub Codespaces development environment in Cortex
  XSIAM.
---

# Set up a GitHub Codespace environment

This topic provides step-by-step instructions for setting up a personal Codespace for developing Cortex XSIAM content.

### **What are GitHub Codespaces?**

[GitHub Codespaces](https://github.com/features/codespaces) are cloud-based development environments provided by GitHub that allow you to set up remote environments with preinstalled and preconfigured tools and dependencies using a dev container.

Your Codespace environment is hosted on GitHub's servers (attached to your GitHub account), and allows you to access your Codespace from any computer.

**Cost and limitations**

GitHub offers a free quota for Codespaces (which is higher for GitHub Pro users) that you can utilize for developing Cortex XSIAM content.

The quota is calculated based on the number of hours your Codespace is actively running. You can see the free quota plan and options for additional paid usage after you reach your quot, in the [GitHub documentation](https://docs.github.com/en/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces#monthly-included-storage-and-core-hours-for-personal-accounts).

You will receive an automated email notification when you have used 75%, 90%, and 100% of your free quota. You can find information about your Codespaces quota usage in the GitHub settings under **Billing and plans**. For more information, see the GitHub article [Viewing your GitHub Codespaces usage](https://docs.github.com/en/billing/managing-billing-for-github-codespaces/viewing-your-github-codespaces-usage).

{% hint style="info" %}
### Note

Codespaces generated from the content repository (or a fork of it) are configured to have four cores by default.
{% endhint %}

### **Create a new Codespace**

1. Log in to your GitHub account. If you do not have a GitHub account, you must create one before you can create a Codespace.
2. Enter the [content repository](https://github.com/demisto/content).
3. Fork the repository to your account.
   1. Click **Fork** at the top right.
   2. Select your account as the owner, and leave the repository name as is.
   3. Keep the **Copy the master branch only** option selected.
   4.  **Create fork**.

       ![content-new-fork-codespace.gif](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-5782cbe2974b2fc44c8181627f4ba0d8eb720716%2F4dc1d2ed3436678156f9bc7bc67df0267e2c878844d31744a8d5429682cab448.gif?alt=media)
4. After a few seconds, you are redirected to your forked repository page.
5. Create a new branch on your fork, and give it a meaningful name.
6.  Click **Code**, go to the **Codespaces** tab, and **Create Codespace on \branch name>**.

    ![create-a-new-codespace.gif](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-8f556bcf6f32d8d41940163c43e513421a27d11c%2F81d67d7800b73a29e901a8131f049ebfe2fffe52e96bbf4a7c4ff903f2bbda50.gif?alt=media)

    If the message **This Codespace is requesting additional permissions** appears, **Continue without authorizing**.
7.  Click **New Codespace**.

    This may take a few minutes to complete.

### **Configure an IDE**

<details>

<summary>Browser-based Visual Studio Code</summary>

By default, GitHub provides a browser-based Visual Studio Code editor that's automatically configured, authenticated, and connected to your Codespace, using your GitHub account.

To open the editor, enter the main forked repository page, click **Code**, go to the **Codespaces** tab, and click the newly created Codespace (should have a random name).

It can take a few minutes for the Codespace to be fully initialized. This delay only occurs the first time you open a Codespace.

Once the initialization is completed and your Codespace is ready, you are redirected to the IDE, where you can start your development.

![open-codespace-in-browser.gif](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-86d0671754c4961feb01143c7e89ea0f4d6c992c%2F76cb85f138ac09395b636163fea9311227e40a6e21db11bf08a11900d90204b0.gif?alt=media)

</details>

<details>

<summary>Visual Studio Code (local)</summary>

To connect to your Codespace from a local Visual Studio Code editor and use the [Visual Studio Extension](visual-studio-code-extension), you need to install the official [GitHub Codespaces extension](https://marketplace.visualstudio.com/items?itemName=GitHub.Codespaces).

For a complete installation and configuration tutorial, refer to the [Using GitHub Codespaces in your local development environment](https://docs.github.com/en/codespaces/developing-in-codespaces/using-github-codespaces-in-visual-studio-code) article by GitHub. You can skip the **Creating a Codespace in VS Code** section, as we've already created a Codespace.

</details>

<details>

<summary>JetBrains IDEs (PyCharm, IntelliJ IDEA, etc.) (local)</summary>

To connect to your Codespace from a JetBrains IDE, you will need to install and configure [JetBrains Gateway](https://www.jetbrains.com/remote-development/gateway).

For a complete installation and configuration tutorial, refer to the official [Using GitHub Codespaces in your JetBrains IDE](https://docs.github.com/en/codespaces/developing-in-codespaces/using-github-codespaces-in-your-jetbrains-ide) article by GitHub.

</details>

**Development**

After your IDE is connected to your Codespace, you can start developing your content. The environment comes pre-installed with all the required tools and dependencies for developing Cortex XSIAM content. Configuring SSH keys or any other credentials is not required, as the Codespace is already authenticated using your GitHub account.

**Additional Resources**

For additional documentation about GitHub Codespaces, see the official [GitHub Codespaces documentation](https://docs.github.com/en/codespaces).
