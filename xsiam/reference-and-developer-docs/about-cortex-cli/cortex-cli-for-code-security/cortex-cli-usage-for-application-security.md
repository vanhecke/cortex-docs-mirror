# Cortex CLI usage for Cortex Cloud Application Security

## Run Cortex Cloud Application Security scans

To scan Cortex Cloud Application Security, run:

```programlisting
cortexcli –-api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --api-key-id <API Key ID> code scan --directory {{DIRECTORY}} --branch main --repo-id organization/repo-name –output json --output-file-path ./output.json
```

## Command line structure

The command structure includes global flags which are used for authentication, and then specifies the module name and command specific to Cortex Cloud Application Security which are followed by dedicated flags unique to this module as well as flags common to all modules.

*   **Global flags**: These flags are part of the initial `cortexcli` command and are necessary to authenticate and connect to Cortex Cloud

    * `--api-base-url`: (Required = true). The public facing API URL. Refer to [Connect Cortex CLI](../connect-cortex-cli) for more information
    * `--api-key`: (Required = true). The Cortex Cloud API key generated when onboarding the CLI as a data source. Refer to [Connect Cortex CLI](../connect-cortex-cli) for more information
    * `--api-key-id`: (Required = true). The Cortex Cloud API key ID generated when onboarding the CLI as a data source

    For a comprehensive list of Cortex Cloud Application Security global flags, refer to [Cortex CLI Cortex Cloud Application Security command line reference](cortex-cli-application-security-command-line-reference)
* **Cortex Cloud Application Security specifics**: Following the global flags, the command specifies the module and the commands required for initiating a scan using the Cortex Cloud Application Security module:
  * `code scan`: Required - true. This command instructs the CLI to perform an Cortex Cloud Application Security scan.
  * For the optional flags, refer to the dedicated Cortex Cloud Application Security [command line reference](cortex-cli-application-security-command-line-reference)

## CLI usage examples

*   **Send output to a file**: Direct the command's output to a specified file instead of displaying it in the console

    ```programlisting
    ./cortexcli --api-base-url <BASE_URL> --api-key <API_KEY> --api-key-id <API_KEY_ID> code scan --branch <branch name> --repo-id <repo name> --directory <path> --output json --output-file-path <path>
    ```
*   **Perform a scan without upload**: Run a scan for local analysis or testing without uploading the results to Cortex Cloud. This command runs a code scan and saves all standard output (human-readable format) to `scan_results.txt`

    ```programlisting
    ./cortexcli --api-base-url <BASE_URL> --api-key <API_KEY> --api-key-id <API_KEY_ID> code scan --upload-mode no-upload --branch <branch name> --repo-id <repo name> --directory <path>
    ```

#### Sample outputs

The `cortexcli` provides different options for how scan results are presented.

* **Standard output** (stdout): When no specific output format flags (such as `--output json` or `--output sarif)` are provided, the Cortex CLI will produce standard output directly to your terminal or console
* **JSON output**: To obtain the output of a scan command as a JSON file, specify the flags `--output json --output-file-path ./output.json`. This command will save the detailed scan results in JSON format to output.json in the current directory.

## Supported flags

The Cortex Cloud Application Security CLI supports both common Cortex CLI and dedicated Cortex Cloud Application Security flags.

* For dedicated Cortex Cloud Application Security flags, refer to [Cortex CLI Cortex Cloud Application Security command line reference](cortex-cli-application-security-command-line-reference)
* For common flags, refer to [Cortex CLI common command line reference guide](../cortex-cli-common-command-line-reference-guide)
