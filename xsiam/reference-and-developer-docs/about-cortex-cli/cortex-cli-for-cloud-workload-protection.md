# Cortex CLI for Cloud Workload Protection

Integrate Cloud Workload Protection (CWP) scans for secrets, vulnerabilities and malware during your continuous integration (CI) process. By leveraging Software Bill of Materials (SBOM) analysis, you can identify and remediate vulnerabilities before images are pushed to the registry, shifting security left and reducing risk in your cloud environments.

{% hint style="warning" %}
### Prerequisites

* Ensure you have the required user permissions. Refer to [Cortex CLI]() for more information
* Onboard and install the Cortex CLI. Refer to [Connect Cortex CLI](connect-cortex-cli) for more information
* Verify that `Java` version 11 and above is installed: Run `java -version` in your terminal. If not, refer to [Java SE Development Kit 11.0.25](https://www.oracle.com/java/technologies/downloads/#java11?er=221886) for information about installing Java
{% endhint %}

## Run CWP security scans

The `cortexcli image scan` command allows you to perform CWP scans on container images. By default, `cortexcli` scans images directly from your local Docker daemon's repository. You can also specify an image archive file to scan instead.

### Prerequisite

Before you begin, ensure you have `sudo` privileges to execute the image scan.

{% hint style="info" %}
### Note

CWP does not support container image secret scanning for systems running on ARM architecture.
{% endhint %}

### Scan from local Docker daemon

For direct scanning from your Docker daemon, the image must already exist in your local Docker repository. The CLI will not pull a new image if it does not exist locally.

To scan an image that exists in your local Docker daemon, simply provide its name:

```programlisting
./cortexcli --api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --api-key-id <API key ID from the "Authenticate" step in the CLI connector screen> image scan <image name>    
```

The image scan accepts the following arguments:

* `--api-base-url`: Required - true. The public facing API URL. Refer to [Connect Cortex CLI](connect-cortex-cli) for more information
* `--api-key`: Required - true. Your Cortex Cloud API key. Refer to [Connect Cortex CLI](connect-cortex-cli) for more information
* `--api-key-id`: Required - true. Your Cortex Cloud API key ID
* `image scan`: Required - true. Refers to CWP as the type of scan

{% hint style="info" %}
### Note

For available CWP commands, refer to [Cloud Workload Protection command line reference](cortex-cli-for-cloud-workload-protection/cloud-workload-protection-command-line-reference).
{% endhint %}

EXAMPLE

```programlisting
./cortexcli --api-base-url https://api.cortex.example.com --api-key your-api-key --api-key-id 1 image scan docker.io/library/nginx:latest
```

EXAMPLE

```programlisting
./cortexcli --api-base-url https://api.cortex.example.com --api-key your-api-key --api-key-id 1 image scan --docker-host unix:///var/snap/docker/common/run/docker.sock my-custom-image:latest
```

By default, Cortex Cloud looks for the Docker socket at `unix:///var/run/docker.sock`.

`--docker-host <path>` specifies the path to the Docker socket. Use this flag if your Docker socket is located elsewhere, for example `unix:///var/snap/docker/common/run/docker.sock`.

### Scan from an image archive file

{% hint style="warning" %}
### Danger

Before you begin, ensure you have sudo privileges to execute the image scan.
{% endhint %}

To scan an image from a previously saved archive file (such as a .tar file), use the `--archive` flag:

```programlisting
./cortexcli --api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --api-key-id <API key ID from the "Authenticate" step in the CLI connector screen> image scan --archive <archive file of container image>
```

{% hint style="info" %}
### Note

* `--archive`: When used with image scan, sets the scan source to an archive file. When used with image sbom, indicates the SBOM should be exported from an archive file
* The `--archive` flag can also be explicitly set as `--archive=true`
* `--archive-format <value>`: The image archive format (such as `docker-archive` or `oci-archive`). Default: `docker-archive`.
{% endhint %}

### Create an image archive

This example demonstrates how to create an image archive from your Docker or Podman environment, which can then be used for scanning or SBOM generation if you choose not to scan directly from the local daemon.

* With Docker: `docker save -o ubuntu.tar ubuntu`
* With Podman: `podman save --format oci-archive -o /tmp/alpine-oci.tar alpine:latest`

## Export SBOM

You can generate a Software Bill of Materials (SBOM) for your container images using the Cortex CLI and and save the output to a specified file. This functionality enables you to store the SBOM for further analysis, auditing, and compliance.

### Export SBOM from local Docker daemon

To export an SBOM for an image from your local Docker daemon:

```programlisting
./cortexcli --api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --api-key-id <API key ID from the "Authenticate" step in the CLI connector screen> image sbom <image name> [command options]
```

**Command**: `cortexcli image sbom`: Exports a Software Bill of Materials (SBOM) document for a container image archive.

**Usage**: `cortexcli image sbom [command options]`

**Options**:

* `--archive-format value`: Specifies the image archive format. Values: `docker-archive` (default), `oci-archive`
* `--output-format value`: Specifies the SBOM document output format. Values: `json` (default), `xml`
* `--output-file value`: Specifies the path to the file where the SBOM document will be saved
* -`-fields value` `[--fields value]`: Specifies the fields to include in the SBOM document. Multiple fields can be specified including: author, binaries, license, name, purl, sourcePackage, type, version
* -`-help`, `-h`: Displays help information for the command

EXAMPLE

```programlisting
./cortexcli --api-base-url https://api.cortex.example.com --api-key your-api-key --api-key-id 1 image sbom docker.io/library/alpine:latest
```

### Export from an image archive

To export an SBOM from an image archive file, use the `--archive` flag:

```programlisting
./cortexcli --api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --api-key-id <API key ID from the "Authenticate" step in the CLI connector screen> image sbom --archive <archive file of container image>
```

**NAME**: `cortexcli image sbom` - Exports an SBOM document for an image from the local Docker daemon or an image archive.

**USAGE**: `cortexcli image sbom` \[command options] \[image name or archive file].

## Troubleshooting

* **Docker socket not reachable**: If you encounter errors indicating the Docker socket cannot be reached, ensure the Docker daemon is running and verify the path to your Docker socket. If it's not in the default location (`unix:///var/run/docker.sock`), use the `--docker-host` flag to specify the correct path
* **Image not found**: If you attempt to scan an image directly from the Docker daemon and receive an error that the image does not exist, confirm that the image is indeed present in your local Docker repository by running `docker images`. The CLI will not pull images
