---
description: >-
  Configure Cortex CLI credentials using a file, environment variables, or
  command-line flags.
---

# Authenticate credentials

Configure credentials before running Cortex CLI. The installer does not save them.

Choose the method that fits your workflow:

* Use a configuration file for persistent local authentication.
* Use environment variables for CI/CD pipelines.
* Use command-line flags for one-off commands or overrides.

Generate API keys in the UI, or use the self-service workflow to create role-restricted CLI and IDE keys through the Public API. The self-service workflow uses a Primary API key. See [Self-service API keys for CLI scans](self-service-api-keys-for-cli-scans).

{% hint style="warning" %}
Do not commit API keys or credential files to source control.
{% endhint %}

### Configuration file

Use a `cortex.env` file for persistent local authentication. Cortex CLI reads this file automatically from your home or current working directory.

The file uses `KEY=VALUE` pairs.

#### macOS and Linux

Create `~/cortex.env` and restrict access to it.

```shell
cat > ~/cortex.env << EOF
CORTEX_API_BASE_URL=https://api-<TENANT>.xdr.us.paloaltonetworks.com
CORTEX_API_KEY=<YOUR_API_KEY>
CORTEX_API_KEY_ID=<YOUR_KEY_ID>
EOF
chmod 600 ~/cortex.env
```

#### Windows

Create `cortex.env` in your user profile.

```powershell
$configPath = "$env:USERPROFILE\cortex.env"
@"
CORTEX_API_BASE_URL=https://api-<TENANT>.xdr.us.paloaltonetworks.com
CORTEX_API_KEY=<YOUR_API_KEY>
CORTEX_API_KEY_ID=<YOUR_KEY_ID>
"@ | Out-File -FilePath $configPath -Encoding UTF8
```

### Environment variables

Use environment variables for CI/CD pipelines. Store values in your CI/CD platform's secret store.

| Variable name         | Description                                                               |
| --------------------- | ------------------------------------------------------------------------- |
| `CORTEX_API_BASE_URL` | Your tenant URL (such as https://api-example.xdr.us.paloaltonetworks.com) |
| `CORTEX_API_KEY`      | The secret key token                                                      |
| `CORTEX_API_KEY_ID`   | The ID associated with the key                                            |

#### macOS and Linux

```shell
export CORTEX_API_BASE_URL="https://api-<TENANT>.xdr.us.paloaltonetworks.com"
export CORTEX_API_KEY="<YOUR_API_KEY>"
export CORTEX_API_KEY_ID="<YOUR_KEY_ID>"
```

#### Windows

```powershell
$env:CORTEX_API_BASE_URL="https://api-<TENANT>.xdr.us.paloaltonetworks.com"
$env:CORTEX_API_KEY="<YOUR_API_KEY>"
$env:CORTEX_API_KEY_ID="<YOUR_KEY_ID>"
```

### Command-line flags

Use flags for one-off scans or to override configured credentials. Place global flags before the module name.

```shell
cortexcli --api-base-url <URL> --api-key <KEY> --api-key-id <ID> code scan ...
```
