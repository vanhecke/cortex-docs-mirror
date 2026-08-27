---
description: >-
  Manage Cortex CLI installations and updates for security scans in Cortex
  XSIAM.
---

# Manage the CLI after installation

Manage Cortex CLI with a package manager or download script. Use either method in CI/CD pipelines or local environments.

## Package managers

### macOS and Linux

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

### Windows

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

## Automate binary downloads

Use this script for a manual installation. It downloads the latest release for your operating system and architecture. Replace your existing binary with the downloaded file. On macOS and Linux, make it executable with `chmod +x`.

```programlisting
crtx_resp=$(curl --fail "<CORTEX_API_URL>/public_api/v1/unified-cli/releases/download-link?os=<OS>&architecture=<ARCH>" \
  -H "x-xdr-auth-id: <AUTH_ID>" \
  -H "Authorization: ${CORTEX_API_KEY}") \
  && crtx_url=$(echo $crtx_resp | jq -r ".signed_url") \
  && crtx_file=$(echo $crtx_resp | jq -r ".file_name") \
  && curl -o $crtx_file $crtx_url
```

### Replace the placeholders

* `CORTEX_API_KEY`: Your API key
* `<CORTEX_API_URL>`: Your tenant API base URL
* `<AUTH_ID>`: Your API key ID value
* `<OS>`: Your operating system — `linux`, `darwin`, or `windows`
* `<ARCH>`: Your system architecture — such as `amd64` or `arm64`

For credential configuration options, see [Authenticate credentials](authenticate-credentials).

### How the script works

The script:

1. Requests a signed download link from Cortex Cloud for the latest release matching your OS and architecture.
2. Uses `jq` to extract the signed URL and binary filename.
3. Downloads the binary from the signed URL.
