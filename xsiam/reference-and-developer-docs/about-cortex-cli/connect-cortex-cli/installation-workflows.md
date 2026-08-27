---
description: Install Cortex CLI for security scans in Cortex XSIAM.
---

# Installation workflows

Choose the installation workflow that fits your environment.

[Before installing the CLI, complete the prerequisites.](..#prerequisites)

## Install through a package manager

Using a package manager is the recommended method for installing the Cortex CLI. Use `Homebrew` for macOS and Linux, or `Scoop` for Windows.

### Homebrew for macOS and Linux

Supported on macOS, Apple Silicon and Intel, and Linux, x86\_64 and arm64.

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

## Manual download

You can manually download the binaries for macOS, Linux, or Windows.

Download the archive from the [releases page](https://github.com/PaloAltoNetworks/homebrew-cortexcli/releases). Verify it against `SHA256SUMS`, then extract it.

| Step              | macOS / Linux                                             | Windows                                                                                  |
| ----------------- | --------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Download**      | Download the `.tar.gz` archive for your architecture      | Download the `.zip` archive                                                              |
| **Extract**       | The executable is named `cortexcli`                       | The executable is named `cortexcli.exe`                                                  |
| **Add to `PATH`** | Move `cortexcli` to a directory such as `/usr/local/bin/` | Move `cortexcli.exe` to a dedicated folder. Add that folder to **Environment Variables** |

## UI-based installation

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

Configure credentials before running scans. See [Authenticate credentials](authenticate-credentials).
