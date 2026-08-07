# Cortex CLI for Code Security

Cortex CLI for Code Security scans allow developers and security teams to integrate security checks directly into their application development workflows.

The Code Security CLI supports the following scan types:

* **Secrets**: Identifies exposed sensitive secrets within your codebase
* **Infrastructure-as-Code** (IaC): Analyzes infrastructure configuration files to detect potential security misconfigurations
* **Software Composition Analysis** (SCA): Performs vulnerability detection in third-party dependencies, assesses their license compliance and their package operational risk

In addition, the Code Security CLI serves as the integration mechanism for security scanning within supported CI tools such as Jenkins, GitHub Actions, and others. This is achieved by adding a code snippet containing the CLI command into the configuration files of your CI tool when integrating the CI tool with Cortex Cloud. It acts as a wrapper, enabling security scanning within your pipelines, and direct upload of results to the platform.

## Code Security CLI scan behavior and output

* Scans generate assets (see [Code Security assets](../../detect-investigate-and-respond-to-threats/asset-management/asset-classes/code-and-ci-cd-assets), [issues](../../detect-investigate-and-respond-to-threats/asset-management/asset-classes/code-and-ci-cd-assets), and [findings](../../detect-investigate-and-respond-to-threats/asset-management/asset-classes/code-and-ci-cd-assets)
* If one scanner (such as Secrets) fails, the other scanners will continue to run and produce results
* Scan failures trigger an error message indicating the scanner that failed
*   The Code Security CLI provides these output modes for management and viewing of scan results:

    * **Upload to platform**: `--upload-mode = upload` (default). Uploads scan results directly to the platform for centralized analysis and management
    * **Upload findings only**. `--upload-mode = no-code`. Upload findings, but without including the actual source code content. This prevents raw source code from leaving your local environment or being stored on the platform
    * **CLI output only**: `--upload-mode=no-upload`. View scan results directly in your command-line interface without being uploaded to the platform

    For more information about the output flags, refer to [Cortex CLI Cortex Cloud Application Security command line reference](cortex-cli-for-code-security/cortex-cli-application-security-command-line-reference).

### Supported outputs

The CLI supports the following outputs:

* json
* spdx
* cli
* junitxml
* sarif
* cyclonedx
* cyclonedx\_json

## Authentication

To authenticate the Code Security CLI, choose one of the following methods:

*   **Local developer workflows**: Run manual, ad-hoc scans on your local machine to catch vulnerabilities and misconfigurations before committing code to your version control system

    The following flags are required to authenticate the Code Security CLI:

    * `--api-base-url`: \[$CORTEX\_API\_BASE\_URL]
    * `--api-key`: \[$CORTEX\_API\_KEY]
    * `--auth-id`. \[$CORTEX\_AUTH\_ID]

    For more information about these flags, refer to [Cortex CLI common command line reference guide](cortex-cli-common-command-line-reference-guide).
* **Using a `cortex.env` file**: Place your authentication details in a `cortex.env` file. You can download this file from the UI
* **CI/CD pipeline automation**: The Application Security CLI serves as the core integration mechanism for security scanning within your automated pipelines. By inserting simple code snippets into CI tools like Jenkins, GitHub Actions, CircleCI, or GitLab Runner, the CLI acts as a wrapper to enforce security guardrails dynamically and block risky deployments

## Requirements

* **For the Cortex CLI binary**:
  * Install `Node.js v22` on the host machine before running scans. The Cortex CLI requires Node.js for JavaScript analysis
    * Check the installed version with `node -v`
    * Download Node.js from the official [Node.js](https://nodejs.org/) site.
  * On Linux systems, install **GLIBC** (GNU C Library) version 2.35 or later. This does not apply when using the CLI container image
* **Permissions**: Ensure you have the required user permissions. Refer to [Cortex CLI]()
* **Onboard and install the Cortex CLI**: Refer to [Connect Cortex CLI](connect-cortex-cli)

## Configure proxy for the Code Security CLI

When operating the Code Security CLI within environments requiring internet access via a proxy server, you can configure the tool to route its traffic through your proxy using standard environment variables. For proxies that perform TLS inspection, you must also specify a CA certificate

* **Environment variables**: Set `HTTP_PROXY` and `HTTPS_PROXY` (or `http_proxy` and `https_proxy`) to your proxy address
* **CA Certificate**: Use the `--ca-certificate` flag or the `$CORTEX_CA_CERTIFICATE` environment variable to provide your CA certificate for proxies that perform TLS inspection. The flag is now global and must appear before `code scan`. It is currently limited to the Application Security CLI. You can either:
