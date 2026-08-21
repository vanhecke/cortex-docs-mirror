---
description: >-
  Configure required Cortex XSIAM network resources for FedRAMP and US federal
  government deployments.
---

# FedRAMP and US federal Cortex XSIAM required resources

Configure firewall access for FedRAMP and US federal government Cortex XSIAM deployments. The following tables list required FQDNs, IP addresses, ports, and App-ID coverage.

### Cortex XSIAM egress and engine resources

All ports are 443 unless otherwise specified.

| Source                   | Compliance Level                     | IP Addresses                         |
| ------------------------ | ------------------------------------ | ------------------------------------ |
| Egress                   | FedRAMP Moderate                     | 34.122.220.113, 35.223.83.172        |
| FedRAMP High             | 34.136.155.252, 34.133.46.50         | ​                                    |
| Outbound IPs for Engines | FedRAMP Moderate                     | 34.123.127.174:443, 34.71.135.18:443 |
| FedRAMP High             | 34.123.153.175:443, 35.223.253.2:443 | ​                                    |

### Core Cortex XSIAM communication resources

These resources handle agent registration, heartbeats, data uploads, and API connections. All ports are 443 unless specified otherwise.

| Resource/Function                                                                                                                                                                                            | FQDN                                                 | IP Address & Port | App-ID                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- | ----------------- | -------------------------- |
| Initial registrationUsed for the first request in registration flow where the agent passes the distribution ID and obtains the **`ch-`**_**`<tenant-name>`**_**`.traps.paloaltonetworks.com`** of its tenant | `distributions-prod-fed.traps.paloaltonetworks.com`  | 104.198.132.24    | `traps-management-service` |
| Agent heartbeat and data uploadUsed for all other requests between the agent and its tenant server, including heartbeat, uploads, action results, and scan reports.                                          | `ch-<tenant-name>.traps.paloaltonetworks.com`        | 130.211.195.231   | `traps-management-service` |
| EDR data uploadUsed for EDR data upload.                                                                                                                                                                     | `dc-<tenant-name>.traps.paloaltonetworks.com`        | 130.211.195.231   | `traps-management-service` |
| API gatewayUsed for API requests and responses.                                                                                                                                                              | `api-<tenant-name>.xdr.federal.paloaltonetworks.com` | 130.211.195.231   | N/a                        |
| Verdict requestsUsed for get-verdict requests.                                                                                                                                                               | `cc-<tenant-name>.traps.paloaltonetworks.com`        | 35.222.50.74      | `traps-management-service` |
| Live terminalUsed in live terminal flow.                                                                                                                                                                     | `wss://lrc-fed.paloaltonetworks.com`                 | 35.188.188.91     | `cortex-xdr`               |
| App proxy                                                                                                                                                                                                    | `app-proxy.federal.paloaltonetworks.com`             | 35.186.217.42     | N/a                        |

### Cortex XSIAM content updates and GCP storage

These resources are hosted on Google Cloud Platform. All ports are 443 unless otherwise specified.

| Resource/function                                                                                                      | FQDN                                                            | IP Addresses     |              |
| ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | ---------------- | ------------ |
| <p><br></p>                                                                                                            | FQDN                                                            | IP Addresses     | App-ID       |
| InstallersUsed to download installers for upgrade actions from the server.                                             | `panw-xdr-installers-prod-fr.storage.googleapis.com`            | IP ranges in GCP | `cortex-xdr` |
| Legacy payloadsUsed to download the executable for the live terminal for Cortex XDR agents earlier than version 7.1.0. | `panw-xdr-payloads-prod-fr.storage.googleapis.com`              | IP ranges in GCP | `cortex-xdr` |
| Content updatesUsed to download content updates.                                                                       | `global-content-profiles-policy-prod-fr.storage.googleapis.com` | IP ranges in GCP | `cortex-xdr` |
| Scanning verdictsUsed to download extended verdict request results in scanning.                                        | `panw-xdr-evr-prod-fr.storage.googleapis.com`                   | IP ranges in GCP | `cortex-xdr` |

### Cortex XSIAM Broker VM resources

Required only for deployments utilizing Broker VM features. All ports are 443, unless otherwise stated.

| Resource/Function                                                                                                                       | FQDN                                                | IP Addresses   |           App-ID           |
| --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------------- | :------------------------: |
| Broker connection                                                                                                                       | `br-<tenant-name>.xdr.federal.paloaltonetworks.com` | 34.71.185.11   |             N/a            |
| <p>Registration</p><p>Used for the first request in the registration flow, for Broker VMs to obtain their specific connection URLs.</p> | `distributions-prod-fed.traps.paloaltonetworks.com` | 104.198.132.24 | `traps-management-service` |
| <p>XSIAM gateway</p><p>Broker VM 3.0 and above</p>                                                                                      | `xsiam-gateway`                                     | N/a            |             N/a            |
| <p>Time sync (NTP)</p><p>Used by the Broker VM to ensure accurate timestamping for forwarded logs.</p>                                  | N/a                                                 | UDP port 123   |             N/a            |

### Cortex XSIAM authentication and SSO

Required for administrator login and Single Sign-On. All ports are 443 unless specified

| Resource         | FQDN                            | IP Addresses and Port | App-ID |
| ---------------- | ------------------------------- | --------------------- | :----: |
| Identity service | `identity.paloaltonetworks.com` | 34.107.215.35         |   N/a  |
| Login service    | `login.paloaltonetworks.com`    | 34.107.190.184        |   N/a  |

### Cortex XSIAM ingress for third-party data collection

Allow traffic from these IPs to your network when collecting data from SaaS and Cloud resources.

| IP Addresses                                         | App-ID       |
| ---------------------------------------------------- | ------------ |
| <ul><li>34.68.217.16</li><li>34.69.175.202</li></ul> | `cortex-xdr` |

### Cortex XSIAM log forwarding to a syslog receiver

If you want to send logs to a syslog receiver, you need to enable access to Cortex XSIAM IP addresses for your region in your firewall. For more information, see [Integrate a syslog receiver](../../../post-deployment/data-and-log-forwarding/forward-logs-and-data-from-cortex-xsiam-to-external-services/configure-external-applications-for-forwarding/integrate-a-syslog-receiver).
