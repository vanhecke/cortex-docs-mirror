---
description: >-
  Reference Cortex CLI commands for Cloud Workload Protection scans in Cortex
  XSIAM.
---

# Cloud Workload Protection command line reference

Use these Cloud Workload Protection-specific commands and flags to run scans with the Cortex CLI. Refer to [Cortex CLI common command line reference guide](../cortex-cli-common-command-line-reference-guide) for common flags that apply across all supported modules and global flags shared with Application Security.

| Command                  | Description                                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------------------- |
| `--image scan`           | Scans a container image archive                                                                    |
| `--ci-pipeline-id value` | The CI pipeline identifier                                                                         |
| `--ci-build-id value`    | The CI build identifier                                                                            |
| `--timeout value`        | Timeout (in seconds) after which the scan will be terminated if it has not completed (default: 60) |
| `--output-format value`  | Output format options: `human-readable`, `json` (default: human-readable)                          |
| `--archive-format value` | The image archive format options: `docker-archive`, `oci-archive` (default: docker-archive)        |
| `--name value`           | The name assigned to the image                                                                     |
| `--docker-host <path>`   | Specifies the path to the Docker socket                                                            |
| `--archive`              | Specifies that the image scan should use an archive file                                           |
