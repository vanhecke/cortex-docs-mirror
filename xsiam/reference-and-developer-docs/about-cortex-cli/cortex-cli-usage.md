# Cortex CLI usage

### Run a Cortex CLI scan

Run scans with this command structure:

```shell
cortexcli [global flags] [module name] scan [module flags]
```

Place global flags before the module name. Place module flags after `scan`.

### Command components

* `cortexcli` — The Cortex CLI binary.
*   **Global flags** — Apply across supported modules. Place them between `cortexcli` and the module name.

    * `--api-base-url <value>`
    * `--api-key <value>`
    * `--api-key-id <value>`

    AppSec and CWP support additional global flags. WAAS does not. See the [Cortex CLI common command line reference guide](cortex-cli-common-command-line-reference-guide).
* **Module name** — Select the environment to scan.
  * `api` — API Security. See [Cortex CLI for API Security](cortex-cli-for-api-security).
  * `image` — Cloud Workload Protection (CWP). See [Cortex CLI for Cloud Workload Protection](cortex-cli-for-cloud-workload-protection).
  * `code` — Cortex Cloud Application Security. See [Cortex CLI for Code Security](cortex-cli-for-code-security).
* **Module flags** — Apply to the selected command.
  * [Cortex CLI common command line reference guide](cortex-cli-common-command-line-reference-guide)
  * [Cloud Workload Protection command line reference](cortex-cli-for-cloud-workload-protection/cloud-workload-protection-command-line-reference)
  * [Cortex CLI API Security command line reference guide](cortex-cli-for-api-security/cortex-cli-api-security-command-line-reference-guide)
  * [Cortex CLI Cortex Cloud Application Security command line reference](cortex-cli-for-code-security/cortex-cli-application-security-command-line-reference)

### Examples

#### Global flags

Global flags apply to all modules. Place them between `cortexcli` and the module name.

```shell
# Authenticate and scan with global authentication flags
cortexcli --api-base-url https://api.xdr.us.paloaltonetworks.com --api-key <KEY> --api-key-id <KEY_ID> code scan --directory .
```

#### Global flags for AppSec and CWP

Upload mode, exit-code handling, and log output are not supported by WAAS.

```shell
# Run an AppSec scan in no-upload mode with soft-fail and log output
cortexcli --upload-mode no-upload --soft-fail --no-fail-on-crash --log code scan --directory .
```

#### Cortex Cloud Application Security scan

Scan source code for IaC misconfigurations, SCA vulnerabilities, and secrets:

```shell
# Scan a repository directory and filter results to critical and high severity
cortexcli --upload-mode no-upload code scan --directory /path/to/repo --severity critical,high
```

See [Cortex CLI usage for Cortex Cloud Application Security](cortex-cli-for-code-security/cortex-cli-usage-for-application-security).

#### Cloud Workload Protection scan

Scan a container image for vulnerabilities:

```shell
# Scan a container image with soft-fail enabled
cortexcli --soft-fail image scan --image myapp:latest
```

See [Cortex CLI for Cloud Workload Protection](cortex-cli-for-cloud-workload-protection).

#### API Security scan

Scan APIs for security issues. Global flags (other than authentication) are not supported:

```shell
# Run an API Security scan
cortexcli api scan --api-spec /path/to/openapi.yaml
```

See [Cortex CLI for API Security](cortex-cli-for-api-security).
