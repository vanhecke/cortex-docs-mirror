# Connect Cortex CLI

Connect Cortex CLI to scan supported Cortex Cloud modules and gain insights into your security posture, enabling you to identify, analyze and address potential risks.

## Prerequisites and requirements

### System requirements

{% tabs %}
{% tab title="macOS" %}
On Intel Core i7 Macs, such as Sequoia, install `vectorscan`:

```bash
brew install vectorscan
```
{% endtab %}

{% tab title="Linux" %}
* **RHEL 8.10 and Red Hat UBI 9:** Install `patchelf` and `zstd`.
* **Ubuntu 20:** Install `prefetch`.
*   **Ubuntu linux-amd64:** Install `libhyperscan5`.

    ```bash
    sudo apt install libhyperscan5
    ```
{% endtab %}

{% tab title="Windows" %}
Windows supports AMD64 and ARM64 architectures.

**Cortex Cloud IDE extension**

If you run terminal actions from a Cortex Cloud IDE extension, use Command Prompt. PowerShell is unsupported for these actions.
{% endtab %}
{% endtabs %}

### Utility requirements for cURL-based downloads

Install both `curl` and `jq`. Install `jq` for your platform:

{% tabs %}
{% tab title="macOS" %}
```bash
brew install jq
```
{% endtab %}

{% tab title="Ubuntu or Debian" %}
```bash
sudo apt-get install jq
```
{% endtab %}

{% tab title="Red Hat, CentOS, or Fedora" %}
```bash
sudo yum install jq
```
{% endtab %}

{% tab title="Windows" %}
Download `jq` from [jq GitHub releases](https://github.com/stedolan/jq/releases), or run:

```bash
choco install jq
```
{% endtab %}
{% endtabs %}

### Authentication and permissions

* **API key:** The CLI authenticates with an API key. No CLI roles exist by default. Ensure the key's role has the required permissions
* **API Security level:** Set the API key security level to `Standard`. Scans fail with the `Advanced` level
* **Local scans only:** Use a role with `CLI Read Only` read-only permissions
* **Upload results:** Use a role with `CLI View/Edit` write permissions

For permission details, see [Cortex CLI]().

Configure how the CLI uses your API key in [Authenticate credentials](connect-cortex-cli/authenticate-credentials).

Generate API keys in the UI, or use the self-service workflow to create role-restricted CLI and IDE keys through the Public API. The self-service workflow uses a Primary API key. See [Self-service API keys for CLI scans](connect-cortex-cli/self-service-api-keys-for-cli-scans).

## Installation workflows

You can choose from three main installation workflows:

* [Package manager](installation-workflows#install-through-a-package-manager): The recommended developer workflow. Use Homebrew on macOS or Linux, or Scoop on Windows
* [Manual download](installation-workflows#manual-download): Download binaries directly for any operating system
* [UI-based installation](installation-workflows#ui-based-installation): Download and authenticate the CLI from your tenant

## Post-installation configuration

After installation, you can upgrade, pin, uninstall, or update Cortex CLI through automated downloads. Refer to [manage the CLI](connect-cortex-cli/manage-the-cli-after-installation) for more information.

## Module-specific requirements

### AppSec module support

#### Supported Linux environments

The AppSec module supports these Linux environments:

* **RHEL 10:** Kernel `6.12`, glibc `2.39`
* **Debian 12:** Kernel `6.1.27`, glibc `2.36`
* **Ubuntu 18.04:** Kernel `4.15`, glibc `2.27`
* **Ubuntu 20.04:** Kernel `5.4`, glibc `2.31`
* **Ubuntu 22.04:** Kernel `5.15`, glibc `2.35`
* **Ubuntu 24.04:** Kernel `6.8`, glibc `2.39`

#### SCA requirements

**Runtime requirements**

Install these runtime layers on the host running Cortex Unified CLI:

* **Layer 1 (the baseline):** `Node.js v22+` is enforced. It is required to boot the SCA engine.
* **Layer 2 (per-ecosystem toolchain):** Install the native language runtime or package manager for the code being scanned. Without the matching toolchain, the SCA engine cannot resolve dependencies.

| Scanned project type | Additional toolchain needed locally, beyond Node v22 |
| -------------------- | ---------------------------------------------------- |
| Java (Maven)         | JDK and `mvn`                                        |
| Java (Gradle)        | JDK and `gradle`                                     |
| .NET                 | .NET SDK (`dotnet`)                                  |
| Python               | Python and `pip` or `pipenv`                         |
| Ruby                 | Ruby and `bundler`                                   |
| Go                   | Go toolchain                                         |
| JavaScript/Node      | `npm` or `yarn` (covered by Node v22)                |

**Suppression requirements**

These practices are required for SCA vulnerability suppression:

* Run the CLI from the current working directory. Use its absolute path.
* Set `--repo-id` to `<repo_owner_name>/<repo_name>`.
* Exact match: The `<repo_name>` in your parameter **must** precisely match the exact name of your local directory.

For example, when the working directory is `Users/test/<repo_name>`, use:

```bash
--repo-id <repo_owner_name>/<repo_name>
```

## Troubleshooting

### `cortexcli --version` shows an unexpected version

An older `cortexcli` binary may appear earlier in your `PATH`. This can come from a `.pkg` installer, manual download, or tenant download.

#### Find every installed copy

{% tabs %}
{% tab title="macOS or Linux" %}
```programlisting
which -a cortexcli
```
{% endtab %}

{% tab title="Windows" %}
```programlisting
where.exe cortexcli
```
{% endtab %}
{% endtabs %}

#### Check the package manager location

The package-managed binary should be at one of these locations:

* **macOS with Homebrew:** `/opt/homebrew/bin/cortexcli` or `/usr/local/bin/cortexcli`
* **Linux with Homebrew:** `/home/linuxbrew/.linuxbrew/bin/cortexcli`
* **Windows with Scoop:** `%USERPROFILE%\scoop\shims\cortexcli.exe`

#### Remove the older copy

* **macOS `.pkg` installer:** Run `sudo rm /usr/local/bin/cortexcli`.
* **Manual or tenant download:** Delete the binary path returned by the command.
* **Windows installer:** Uninstall it in **Settings** → **Apps** → **Installed apps**.

Open a new terminal. Then run `cortexcli --version` again.

## Learn more

* [Installation workflows](connect-cortex-cli/installation-workflows)
* [Manage the CLI after installation](connect-cortex-cli/manage-the-cli-after-installation)
* [Authenticate credentials](connect-cortex-cli/authenticate-credentials)
* [Self-service API keys for CLI scans](connect-cortex-cli/self-service-api-keys-for-cli-scans)
