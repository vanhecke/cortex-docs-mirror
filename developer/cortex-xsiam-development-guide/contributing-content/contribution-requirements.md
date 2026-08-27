---
description: >-
  Prerequisite tools and environments for developing content for contributions
  to Cortex XSIAM.
---

# Contribution requirements

There are requirements to develop and contribute content (including integrations and scripts) to Cortex XSIAM. If you are unsure whether this article applies to you, more details can be found in the [getting started](../readme) chapter.

### Cortex XSIAM

You need an active Cortex XSIAM tenant.

### Development operating system

We recommend using macOS or Linux for development, as we use bash and Docker in some of our validation/testing flows. We also support Windows through WSL. For Windows, you can work either with a Linux VM or use Windows Subsystem for Linux.

{% hint style="info" %}
**Note**

When using WSL2 you may experience performance issues if working on the Windows mounted file system (for example `/mnt/c/`). See the following [WSL issue](https://github.com/microsoft/WSL/issues/4197) for more info. In that cases, we recommend using the Linux file system (ext4 partition) WSL2 provides, and the local content and the SDK are located on the WSL file system, using an editor that supports remote WSL. Editors supporting remote WSL include [VS Code](https://code.visualstudio.com/docs/remote/wslPyCharm%20) and [PyCharm Professional Edition](https://www.jetbrains.com/help/pycharm/using-wsl-as-a-remote-interpreter.html).
{% endhint %}

### GitHub

You will need a [GitHub](https://github.com/) account, as the contribution process requires you to submit a pull request in the Cortex XSIAM [content repository](https://github.com/demisto/content). To learn more about pull requests and contributing , check out the [collaborating with issue and pull requests tutorial](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests) on GitHub.

You will also need git - a distributed version control system, installed in your development environment. In the examples, we'll use the git command-line tool. Visit the [Git - Getting Started Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for installation instructions.

### Python

If you are planning on contributing code, (i.e., integrations or scripts) you recommend using Python. While some content is built via JavaScript and Python 2, we require Python 3.7+ for contributions.

We recommend having a dedicated Python 3 installed on your system for development purposes. [Pyenv](https://github.com/pyenv/pyenv) allows you to easily manage multiple versions of Python on your system.

Optionally, macOS users can install via [homebrew](https://docs.brew.sh/Homebrew-and-Python).

While you don't need to be a Python expert to write a good integration, intermediate level Python knowledge is preferred. Be sure to adhere to our [Code Conventions](../integrations-and-scripts/developing/python-code-conventions).

### PowerShell

We also support PowerShell. However, we recommend PowerShell only for advanced users, as the number of content examples is limited.

### Docker

If you are writing code (i.e. integrations and scripts), you need to run several linters and unit tests to validate your code, as we do in our build process. In this case, you must install Docker. Visit the [Docker site installation page](https://docs.docker.com/install/) for installation options. If you're using WSL, you should [enable the integration with Docker Desktop](https://docs.docker.com/desktop/windows/wsl/#enabling-docker-support-in-wsl-2-distros).

### Node.js and npm

(Optional) We use Node.js for validating README documentation files for integrations, scripts and playbooks. If you are creating README documentation files, we recommend installing Node.js to be able to validate the files locally. Node.js installation instructions for your target platform are available at: [https://nodejs.org/en/download/package-manager](https://nodejs.org/en/download/package-manager).
