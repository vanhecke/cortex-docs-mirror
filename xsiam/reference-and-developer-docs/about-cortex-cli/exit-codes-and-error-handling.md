# Exit codes and error handling

The Cortex Unified CLI has standardized exit codes categorized by application states, error suppression flags, and specific modules. Use this guide to configure and troubleshoot your CI/CD pipelines.

**Standard CLI exit codes**

| Exit Code | Constant / Representation                | Description                                                                                                                                                                 |
| --------- | ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`0`**   | `ScanSuccess`                            | The scan executed successfully and no security findings were found                                                                                                          |
| **`1`**   | `ScanFailed`                             | The scan completed with findings (e.g., findings blocked by AppSec policy), or a general operational failure occurred                                                       |
| **`2`**   | `ScanExecutionFailure` / `InternalError` | An execution error occurred, version mismatch was detected (local version is strictly greater than the backend version), or a CLI usage/configuration error was encountered |

***

**Exit code suppression flags**

The CLI provides two global flags to control and suppress exit codes in automated environments:

* **`--soft-fail`**: Converts exit code **`1`** (findings with blocking policy) to **`0`**
* **`--no-fail-on-crash`**: Converts exit code **`2`** (internal/execution error) to **`0`**

**Module-specific exit codes**

**Attestation module**

* **`1` (`exitOperationFailed`)**: Returned when a cryptographic or attachment operation fails (e.g., signing failed, verification failed, register/delete/update key failed, failed to render output).
* **`2` (`exitUsageError`)**: Returned for user configuration/usage errors (e.g., missing required flags like `--image` or `--key`, invalid flag values).

**Code security module**

* **`2` (`casExtractErrorCode`)**: Returned when the runner fails to extract the underlying APPSEC engine, failed to acquire lock, failed to validate signature, or during timeout execution.
