---
description: >-
  Use Visual Studio Code extension to design and author scripts and integrations
  for Cortex XSIAM directly from VS Code.
---

# Visual Studio Code extension

The Cortex XSOAR extension for Visual Studio Code (compatible with both Cortex XSOAR and Cortex XSIAM) enables you to design and author scripts and integrations for Cortex XSIAM directly from VS Code. When writing code, the plugin provides you with auto-completion of Cortex XSIAM and Python functions. The extension also provides an easy-to-use set of demisto-sdk commands to format your packs, lint, and validate. The extension provides an easy virtual environment setup for Cortex XSIAM integrations and scripts.

{% hint style="info" %}
### Note

The content repository from GitHub must be cloned or forked. Do not change the default folder name, which is `content`. The Visual Studio Code extension must be run from inside the content repository folder. If you run the extension from a different folder, the **command 'xsoar.updateDSDK** error appears.
{% endhint %}

**Prerequisites**

* Python 3.9 and up
* [VS Code](https://code.visualstudio.com/Download)
*   Docker

    See the [Visual Studio Code instructions](https://code.visualstudio.com/docs/remote/containers#_installation) for Docker installation.

**Install the Visual Studio Code extension**

Install the Visual Studio Code extension directly from the Visual Studio Code marketplace or use this [link](https://marketplace.visualstudio.com/items?itemName=CortexXSOARext.xsoar). If you are using a Windows machine, click CTRL+SHIFT+P and choose Connect to WSL.

**Configurations**

Cortex XSIAM recommends keeping the `xsoar.autoFindProblems.readProblems` configuration set to `false`, which is the default setting, for improved performance. When this configuration is set to `true`, it automatically runs  `demisto-sdk validate` when saving your file.

**Commands**

All of the commands in the extension start with XSOAR. For example:

* `XSOAR: Demisto-SDK Validate/Update Release Notes...`: Runs the `demisto-sdk` commands.
* `XSOAR: Configure XSOAR unit tests`: Configures the integration unit tests.
* `XSOAR: Configure XSOAR connection`: Configures environment variables for demisto-sdk.

**Environment setup**

**Remote development (Any OS)**

To develop in a fully configured remote development environment, see instructions for a [traditional development environment](set-up-a-local-development-environment) or a [GitHub Codespace](set-up-a-github-codespace-environment). You can also use a [containerized development environment](set-up-a-containerized-development-environment), which includes the Visual Studio Code extension by default.

**Local development (Linux, MacOS, WSL2)**

The VS Code extension supports setting up your development environment automatically. Run the command `XSOAR: install local development environment` from [VS Code Command Pallete](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette) or by right-clicking the file.

If you want to install the dependencies manually, follow the instructions in [this guide](https://github.com/demisto/content-docs/blob/master/docs/concepts/dev-setup.md#option-3-manual-setup) until the Bootstrap step.

**Set up integrations and scripts environment**

Each integration or script in Cortex XSIAM runs on a different environment and has different dependencies. This feature configures the integration or script and allows you to debug it and run unit tests. In addition, you can open the integration environment in a new workspace with a virtual environment, for auto-completion.

**Usage**

1. Navigate to the integration or script.
2. Right-click the integration/script and select **Setup integration/script environment**.
3. A dialog box appears allowing you to choose to the use the current workspace or to open a new one with a virtual environment. Note that using the current workspace is faster, but you may not have auto-completion for some integrations. Opening a new workspace takes longer, but you have auto-completion for all integrations. Both options allow you to debug your integration or script, run unit test, and identify problems from within the IDE.

**Debugging**

1. [Setup integrations and scripts environment](https://github.com/demisto/content-docs/blob/master/docs/concepts/vscode-extension.md#open-integrations-and-scripts-in-python-virtual-environment).
2. Read the [Debugging using your IDE](https://github.com/demisto/content-docs/blob/master/docs/integrations/debugging#Debugging%20using%20your%20IDE) section.
3. Go to **Run and Debug** (⇧⌘D), and verify `Docker: debug (<integration>)` is selected.
4. Click on the green arrow or the F5 key to begin debugging.

{% hint style="info" %}
### Note

If during the installation one or more Python packages fails to install, the installation proceeds and creates the virtual environment with the packages that were installed.
{% endhint %}

**Troubleshooting**

**Setup integration/script environment fails**

* Verify Docker is running.
* Verify the **Allow the default Docker socket to be used (requires password)** option is enabled in Docker advanced settings.
* If Docker is running, follow instructions to [prune unused Docker objects](https://docs.docker.com/config/pruning/) and/or [sign in to Docker](https://www.docker.com/blog/seamless-sign-in-with-docker-desktop-4-4-2/) to avoid the [Docker pull rate limit](https://docs.docker.com/docker-hub/download-rate-limit/).
