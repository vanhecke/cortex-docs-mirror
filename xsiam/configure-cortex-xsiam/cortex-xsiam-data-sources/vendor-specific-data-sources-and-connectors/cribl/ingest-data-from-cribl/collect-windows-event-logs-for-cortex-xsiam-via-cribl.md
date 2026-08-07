# Collect Windows Event Logs for Cortex XSIAM via Cribl

There are two primary methods for streaming Windows Event Logs to Cortex XSIAM using Cribl. The choice depends on whether you prefer a centralized, agentless architecture or a distributed, agent-based approach.

**Avoid data duplication**: Do not enable both WEF and Cribl Edge on the same endpoint for the same log channels.

For the general Cribl-to-XSIAM integration workflow (credentials, destination, XSIAM pack, and verification), see the [Cribl integration documentation](https://docs.cribl.io/stream/4.7/usecase-wef-config/#configuring-wef-for-cribl-stream).

Comparison of collection methods

| Option | Method             | Description                                                                                                           |
| ------ | ------------------ | --------------------------------------------------------------------------------------------------------------------- |
| A      | Cribl Stream + WEF | **Agentless**: Cribl Stream acts as the Windows Event Collector. Endpoints forward events via mutual TLS (port 5986). |
| B      | Cribl Edge         | **Agent-based**: The Cribl Edge agent is installed on every endpoint to read local logs directly.                     |

### Optional A: Windows Event Forwarding (Agentless)

Use this method if you want to avoid installing software on every Windows endpoint. This requires existing Windows-side configurations for certificates and Group Policy. Cribl Stream receives Windows events directly from endpoints using the Windows Event Forwarder Source with mutual TLS authentication.

Windows endpoints must be configured to forward events to Cribl Stream. For the Windows-side configuration (certificate generation, Group Policy, Subscription Manager), see [Cribl WEF Configuration Guide](https://docs.cribl.io/stream/4.4/usecase-wef-config/).

#### Task 1. Import the CA Certificate

Import the CA certificate that signed the client certificates on the Windows endpoints.

1. In the Cribl Stream Worker Group UI, select Settings → Security → Certificates → New Certificate.
2.  Cribl Stream requires every CA certificate to be accompanied by a cert/key pair. Generate a placeholder pair:

    ```
    openssl req -x509 -newkey rsa:2048 -nodes -keyout key.pem -out cert.pem -sha256 -days 365 -subj "/CN=placeholder"
    ```
3. Configure the certificate:
   * Certificate: Paste the placeholder `cert.pem` contents.
   * Private key: Paste the placeholder `key.pem` contents.
   * CA certificate: Paste the CA certificate PEM from your Windows environment.
4. If the client certificates contain a CA chain (root and intermediate signers), import the entire chain. Concatenate the PEM files in the CA certificate field, ordered from host to root CA.
5. Save the certificate configuration.

#### Task 2. Create the WEF source

1. Select Data → Sources → Push → Windows Event Forwarder → New Source.
2. Configure General Settings:
   * Input ID: Enter a descriptive name, such as wef-windows-events.
   * Address: `0.0.0.0`
   * Port: `5986` (do not change as this is the WEF mTLS port)
   * Authentication method: Client certificate
3. Configure Certificate Settings:
   * Certificate: Select the certificate created in Task 1.
   * Private key path: For Cribl.Cloud, use `/opt/criblcerts/criblcloud.key`
   * Certificate path: For Cribl.Cloud, use `/opt/criblcerts/criblcloud.crt`
4. Configure Advanced Settings:
   * MachineID Mismatch: Set to Yes if using a shared certificate, or No if using auto-enrollment for higher security.

#### Configure subscriptions

1. In the WEF Source configuration, click Subscriptions in the left navigation.
2.  Add the event log channels to collect:

    | Query Path                             | Query Expression |
    | -------------------------------------- | ---------------- |
    | `Security`                             | `*[System]`      |
    | `System`                               | `*[System]`      |
    | `Application`                          | `*[System]`      |
    | `Microsoft-Windows-Sysmon/Operational` | `*[System]`      |
3.  Save, Commit, and Deploy the configuration.

    All settings, including certificate configuration, only take effect after committing and deploying.

### Option B: Cribl Edge Direct Windows Event Collection

Cribl Edge collects Windows Event Logs directly from the endpoint where it is installed.

#### Task 1. Deploy Cribl Edge

1. Download the Cribl Edge MSI from the Cribl portal.
2. Install the Edge agent on the target Windows machine.
3. Verify the Edge node appears in the Cribl Edge interface under Fleet.

#### Task 2. Add a Windows Event Logs Source

1. In the Cribl Edge interface, add a new Windows Event Logs source tile.
2.  Configure the event logs to collect:

    | Event Log Name                         | Description                                               |
    | -------------------------------------- | --------------------------------------------------------- |
    | `Security`                             | Windows Security events                                   |
    | `System`                               | Windows System events                                     |
    | `Application`                          | Windows Application events                                |
    | `Microsoft-Windows-Sysmon/Operational` | Sysmon events (requires Sysmon installed on the endpoint) |



#### Task 3. Configure Optional Settings

Expand the Optional Settings section and set the following:

| Setting      | Value        | Reason                                                                     |
| ------------ | ------------ | -------------------------------------------------------------------------- |
| Read Mode    | `Entire log` | Ensures complete data ingestion from the beginning of the log              |
| Event Format | `XML`        | Guarantees properly structured data for downstream parsing in Cortex XSIAM |

#### Task 4. Save and deply

Save the source configuration and deploy to the Edge node.

<br>

<br>

<br>
