# Connect Cortex CLI

Connect Cortex CLI to scan supported Cortex Cloud modules and gain insights into your security posture, enabling you to identify, analyze and address potential risks.

## Installation workflows

You can choose from three main installation workflows:

* [Package Manager](#workflow-1-install-through-a-package-manager): The most efficient developer workflow, utilizing Homebrew for macOS/Linux and Scoop for Windows
* [Manual download](#workflow-2-manual-download-any-os): Directly download the binaries for any operating system
* [UI-based installation](#workflow-3-ui-based-installation): Onboard and download the CLI directly from your tenant

## Prerequisites

### System requirements

#### macOS

On Intel Core i7 Macs, such as Sequoia, install `vectorscan`:

```bash
brew install vectorscan
```

#### Linux

* **RHEL 8.10 and Red Hat UBI 9:** Install `patchelf` and `zstd`.
* **Ubuntu 20:** Install `prefetch`.
*   **Ubuntu linux-amd64:** Install `libhyperscan5`.

    ```bash
    sudo apt install libhyperscan5
    ```

**AppSec Module support**

The AppSec Module supports these Linux environments:

* **RHEL 10:** Kernel `6.12`, glibc `2.39`
* **Debian 12:** Kernel `6.1.27`, glibc `2.36`
* **Ubuntu 18.04:** Kernel `4.15`, glibc `2.27`
* **Ubuntu 20.04:** Kernel `5.4`, glibc `2.31`
* **Ubuntu 22.04:** Kernel `5.15`, glibc `2.35`
* **Ubuntu 24.04:** Kernel `6.8`, glibc `2.39`

#### Windows

Windows supports AMD64 and ARM64 architectures.

**Cortex Cloud IDE extension**

If you run terminal actions from a Cortex Cloud IDE extension, use Command Prompt. PowerShell is unsupported for these actions.

### Utility requirements for cURL-based downloads

Install both `curl` and `jq`. Install `jq` for your platform:

{% tabs %}
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

{% tab title="macOS" %}
```bash
brew install jq
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

### SCA suppression requirements

These practices are required for SCA vulnerability suppression:

* Run the CLI from the current working directory. Use its absolute path.
* Set `--repo-id` to `<repo_owner_name>/<repo_name>`.
* Exact match: The `<repo_name>` in your parameter **must** precisely match the exact name of your local directory.

For example, when the working directory is `Users/test/<repo_name>`, use:

```bash
--repo-id <repo_owner_name>/<repo_name>
```

## Workflow 1: Install through a package manager

Using a package manager is the recommended method for installing the Cortex CLI. Use `Homebrew` (for macOS and Linux) or `Scoop` (for Windows).

### Homebrew for macOS and Linux

Supported on macOS (Apple Silicon & Intel) and Linux (x86\_64 & arm64).

Requires [Homebrew](https://brew.sh/).

#### Standard installation

```programlisting
brew tap paloaltonetworks/cortexcli
brew install cortexcli
cortexcli --version
```

#### Pin a specific version (optional)

If your workflow requires a specific version, use one of these methods.

**Pin a release line**

For example, stay on the `0.18.x` release line.

This locks the CLI to a minor version. Security patches continue automatically.

```programlisting
brew install cortexcli@0.18
# keg-only — add to PATH if needed:
echo 'export PATH="$(brew --prefix cortexcli@0.18)/bin:$PATH"' >> ~/.zprofile
```

**Pin an exact version**

For example, install exactly `0.18.0`.

This locks the CLI to one build. It prevents automatic updates.

### Scoop for Windows

Supported on Windows x64.

Requires [Scoop](https://scoop.sh/).

#### Standard installation

```programlisting
scoop bucket add cortexcli https://github.com/PaloAltoNetworks/homebrew-cortexcli
scoop install cortexcli
cortexcli --version
```

#### Install a specific version (optional)

If your workflow requires a specific version, use:

```programlisting
scoop install cortexcli@0.18.0
```

## Workflow 2: Manual download (any OS)

You can manually download the binaries for macOS, Linux, or Windows.

Download the archive from the [releases page](https://github.com/PaloAltoNetworks/homebrew-cortexcli/releases). Verify it against `SHA256SUMS`, then extract it.

| Step              | macOS / Linux                                             | Windows                                                                                  |
| ----------------- | --------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Download**      | Download the `.tar.gz` archive for your architecture      | Download the `.zip` archive                                                              |
| **Extract**       | The executable is named `cortexcli`                       | The executable is named `cortexcli.exe`                                                  |
| **Add to `PATH`** | Move `cortexcli` to a directory such as `/usr/local/bin/` | Move `cortexcli.exe` to a dedicated folder. Add that folder to **Environment Variables** |

## Workflow 3: UI-based installation

Install the CLI directly from your Cortex tenant. The UI generates a tenant-specific command that downloads and authenticates the binary.

{% stepper %}
{% step %}
### Generate the installation command

1. Navigate to **Settings** → **Data Sources** → **+ Data Source**.
2. Search for **Cortex CLI**.
3. Select **Connect** or **Connect Another Instance** on the Cortex CLI card.
4. In **Configure**, select your operating system. Then click **Next**.
5. In **Authenticate**, generate an API key.
   * Select **With upload results permissions** to create a **CLI View/Edit** role.
   * Otherwise, the key receives a **CLI Read Only** role with **CLI View** permissions.

{% hint style="info" %}
The Cortex CLI requires an API key with the `Standard` security level.
{% endhint %}

6. Save the generated **API Key ID** and **API key**.
7. Copy the command from **Retrieve your API key**.

{% hint style="info" %}
On macOS ARM64, unpack the download to access the executable.
{% endhint %}

8. Verify the key appears in the API Keys inventory.
{% endstep %}

{% step %}
### Download the CLI

Before you run the command, replace any placeholders with your credentials:

1. Replace `${API_KEY}` with the saved API key.
2. If needed, copy the API URL from **Settings** → **Configurations** → **API Keys**.
3. Paste the completed command into your terminal. Then press Enter.

The generated command follows this syntax:

```programlisting
curl -k -u $CORTEX_API_ID::$CORTEX_API_KEY --output ./cortexcli $CORTEX_FQDN/api/v2/remote-li/{version}/{platform}/artifacts
```

This securely connects to your specific Cortex tenant (`$CORTEX_FQDN`) and downloads the `cortexcli` application directly to your current folder.
{% endstep %}

{% step %}
### Make the CLI executable

On macOS and Linux, allow the downloaded binary to run:

```programlisting
chmod +x cortexcli
```
{% endstep %}

{% step %}
### Verify the installation

Run the command that matches the binary location:

{% tabs %}
{% tab title="On your PATH" %}
```programlisting
cortexcli -v
```
{% endtab %}

{% tab title="Current directory" %}
```programlisting
./cortexcli -v
```
{% endtab %}
{% endtabs %}

If the terminal displays a version, return to Cortex Cloud and click **Done**.
{% endstep %}
{% endstepper %}

## Manage the CLI after installation

After installation, manage the CLI with a package manager or download script. Use either method in CI/CD pipelines or local end-user environments.

### Package managers

#### macOS and Linux

*   **Upgrade to the latest version**

    ```programlisting
    brew upgrade cortexcli
    ```
*   **Pin the installed version**

    ```programlisting
    brew pin cortexcli
    ```
*   **Uninstall the CLI**

    ```programlisting
    brew uninstall cortexcli
    ```

#### Windows

*   **Upgrade to the latest version**

    ```programlisting
    scoop update cortexcli
    ```
*   **Prevent upgrades**

    ```programlisting
    scoop hold cortexcli  
    ```
*   **Allow upgrades again**

    ```programlisting
    scoop unhold cortexcli     
    ```
*   **Uninstall the CLI**

    ```programlisting
    scoop uninstall cortexcli
    ```

### Automate binary downloads

Use this script for a manual installation. It downloads the latest release for your operating system and architecture. Replace your existing binary with the downloaded file. On macOS and Linux, make it executable with `chmod +x`.

```programlisting
crtx_resp=$(curl --fail "<CORTEX_API_URL>/public_api/v1/unified-cli/releases/download-link?os=<OS>&architecture=<ARCH>" \
  -H "x-xdr-auth-id: <AUTH_ID>" \
  -H "Authorization: ${CORTEX_API_KEY}") \
  && crtx_url=$(echo $crtx_resp | jq -r ".signed_url") \
  && crtx_file=$(echo $crtx_resp | jq -r ".file_name") \
  && curl -o $crtx_file $crtx_url
```

#### Replace the placeholders

* `CORTEX_API_KEY`: Your API key
* `<CORTEX_API_URL>`: Your tenant API base URL
* `<AUTH_ID>`: Your API key ID value
* `<OS>`: Your operating system — `linux`, `darwin`, or `windows`
* `<ARCH>`: Your system architecture — such as `amd64` or `arm64`

#### How the script works

The script:

1. Requests a signed download link from Cortex Cloud for the latest release matching your OS and architecture.
2. Uses `jq` to extract the signed URL and binary filename.
3. Downloads the binary from the signed URL.

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
