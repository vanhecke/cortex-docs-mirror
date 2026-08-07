# Cortex XSIAM federal compliance

Cortex XSIAM is FedRAMP **High**- and **Moderate-authorized**, providing a secure environment specifically for U.S. Federal agencies and highly regulated industries.

**Security & infrastructure architecture**

To ensure strict compliance, these environments utilize the following safeguards:

* **Isolation**: Dedicated single-tenant instances that are physically and logically isolated from the commercial user base.
* **Data sovereignty**: All logs and ingested data remain strictly within the United States.
* **Infrastructure**: Usage of government-specific infrastructure, such as AWS GovCloud or Azure Government.
* **Secure egress**: Implementation of federal FQDNs, such as `p-proxy.federal.paloaltonetworks.com`, to secure all egress traffic paths.
* **Scanning rights:** FedRAMP instances are authorized to scan both secure government and standard commercial cloud accounts, whereas commercial instances are strictly prohibited from accessing government-authorized environments.

### Software Composition Analysis (SCA) for FedRAMP

Application Security Software Composition Analysis (SCA) is available in FedRAMP and Government (Gov) tenant environments. Organizations operating under FedRAMP or public-sector compliance requirements can scan open-source dependencies for known vulnerabilities (CVEs), license miscompliance, and package operational risks using the same SCA scanner available in commercial environments.

SCA in FedRAMP/Gov tenants uses the same enablement and prerequisites as commercial tenants:

* The Application Security module is active on the tenant
* At least one VCS integration is onboarded
* The SCA scanner is enabled for the target repositories
* At least one periodic or PR scan has completed

No FedRAMP-specific configuration is required.

For more information on SCA, refer to [Software Composition Analysis (SCA )](https://app.gitbook.com/s/8Z0RLJ1BFF5TQL8VtUeK/software-supply-chain-security/risk-and-remediation/software-composition-analysis-sca-scanners "mention").
