---
description: >-
  Integrate Application Security secrets scanner as pre-commit hooks into your
  workflows to scan for errors on your machine before local commits.
---

# Cortex CLI pre-commit hooks

Integrate the Cortex Cloud Application Security secrets scanner as a pre-commit hook by installing the Cortex CLI. The scanner executes the hook locally before a commit. This setup ensures that secrets checks are enforced before any changes are committed.

When setting up pre-commit hooks, you can choose between local hooks and global hooks.

* **Local**: Installs the hook in the `.git/hooks` directory of the **current** repository, ensuring that Cortex Cloud secrets scans automatically run on your code before every commit
* **Global**: Installs the hook for **all** Git repositories on your machine, so Cortex Cloud secrets scans will automatically run on your code before every commit, regardless of the project

## How to configure pre-commit hooks

{% hint style="warning" %}
### Prerequisite

These common prerequisites are required for all types of installation (both local and global) of the Cortex CLI pre-commit hook.

* Ensure you have a license for Cortex Cloud Application Security
* Install the Cortex Cloud CLI binary locally. Refer to [Connect Cortex CLI](../connect-cortex-cli) for information about onboarding the CLI
* Obtain Cortex Cloud API credentials (API Key ID and API Key) available from the CLI onboarding process (see above), and your API base URL. For more information on creating API keys, refer to [Create a new API key](https://app.gitbook.com/s/1ZrobAtcwfCDWAJAWeuj/create-a-new-api-key)
* **Git**: You must have Git installed on your machine. For installation instructions, refer to the [official Git website](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
{% endhint %}

1.  Create a directory:

    ```programlisting
     mkdir -p ~/.cortexcli
    ```
2. Create a `.cortex.yaml` file in the `~/.cortexcli/` directory.
3.  Open the `.cortex.yaml` file and add your Cortex Cloud API credentials and API base URL to the `yaml` file:

    * `CORTEX_API_BASE_URL`: \<replace with the base API URL>
    * `CORTEX_API_KEY_ID`: \<replace with API Key ID>
    * `CORTEX_API_KEY`: \<replace with API Key>

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>It is recommended you configure credentials for the Cortex CLI using a configuration file.</p></div>
4.  **For local hooks**: Install the Cortex CLI pre-commit hook package to set up a local hook for the current Git repository:

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><h3>Prerequisite</h3><p>For local installation: Install the <strong>pre-commit</strong> framework version 3.2.0 or greater. Refer to <a href="https://pre-commit.com/">https://pre-commit.com/</a> for installation instructions.</p></div>

    1.
       *   For **macOS**, you can use **Homebrew**:

           ```programlisting
            brew install pre-commit
           ```
       *   For other installations run:

           ```programlisting
            pip install pre-commit
           ```
    2.  **Navigate to the root of your repository** → **run the following command**:

        ```programlisting
         cortexcli code pre-commit install --mode local
        ```
5.  **For Global hooks**: Install the Cortex CLI pre-commit hook package to set up hooks for all Git repositories on your machine.

    ```programlisting
    cortexcli code pre-commit install --mode global
    ```

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>The <strong>pre-commit</strong> framework is not required for global mode.</p></div>

## References

To set up the Cortex CLI as a pre-commit hook on supported platforms, refer to the following official Git documentation for managing hooks:

* **Git Hooks**: A comprehensive guide on all available Git hooks, including `Pre-commit`: [https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
* **Atlassian Git Tutorial**: A tutorial that explains the purpose and usage of both local and server-side hooks, including `pre-commit`: [https://www.atlassian.com/git/tutorials/git-hooks](https://www.atlassian.com/git/tutorials/git-hooks)
