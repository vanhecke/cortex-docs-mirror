# Cortex CLI API Security command line reference guide

Use these API Security-specific commands and flags to run scans with the Cortex CLI. Refer to [Cortex CLI common command line reference guide](../cortex-cli-common-command-line-reference-guide) for common flags that apply across all supported modules.

| Value                        | Description                                                                                                                  |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `--scanned-app-url` (string) | Base URL of the app to scan (required)                                                                                       |
| `--api-spec-file` (string)   | Path to the API specification file (required)                                                                                |
| `--api-spec-type` (string)   | Type of the API specification ('openapi) (default "openapi")                                                                 |
| `--auth-file` (string)       | Path to the authentication file (optional). For more information on authentication, refer to [Cortex CLI for API Security]() |
| `--concurrency` (int)        | Concurrency limit for scan requests (default 5)                                                                              |
| `--java-location` (string)   | Path to the Java (version >= 11) binary file (default: Java)                                                                 |
| `--no-publish` (boolean)     | Avoid publish results to Cortex                                                                                              |
| `--output-file` (string)     | Output path for the report file (optional)                                                                                   |
| `--timeout` (int)            | Scan timeout in seconds (default 300)                                                                                        |
| `--zap-port` (int)           | Listening port to be used by ZAP (default 35391)                                                                             |
