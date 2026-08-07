# AWS security model and authentication

Cortex XSIAM implements a defense-in-depth security model built on the principle of least privilege. Every permission granted to Cortex XSIAM is scoped to a specific security capability and has a clear purpose. This section describes the security principles, authentication mechanisms, and operational safeguards that protect your AWS environment.

## **Security principles**

* **Minimal permissions by default:** Cortex XSIAM operates with the minimum permissions necessary for each capability. Discovery and posture assessment rely on read-only access wherever possible. Additional permissions are only provisioned when you explicitly enable optional capabilities such as agentless disk scanning or data security posture management.
* **Capability-scoped write access:** Each optional capability uses a dedicated policy that is attached only when the capability is enabled. Operations that require limited write access, such as creating temporary resources during analysis, do not modify existing customer assets.
* **Permission transparency and health monitoring:** Cortex XSIAM continuously validates that all required permissions remain granted. Every entitlement is mapped to a purpose description so you understand why each permission is required. Missing or revoked permissions are displayed as health status warnings in the connector dashboard.

## **Authentication mechanisms**

Cortex XSIAM eliminates the risk of leaked credentials by strictly avoiding static IAM Access Keys, instead relying on temporary, short-lived tokens provided by the AWS Security Token Service (STS). Three isolated identity flows ensure that discovery, scanning, and logging operations remain functionally and cryptographically separated.

* **Discovery and scan flows:** These flows use cross-account AssumeRole calls. These calls include a mandatory sts:ExternalId condition to prevent "confused deputy" attacks, ensuring only your specific Cortex XSIAM tenant can access your roles.
* **Audit logs flow:** Employs OIDC Federation through AssumeRoleWithWebIdentity. AWS natively validates Google-signed OIDC tokens from Cortex (GCP), which facilitates a secure identity handshake without the need for manual Identity Provider (IdP) management.
* **Cloud-native identity and trust:** Deployment uses cloud-provider-native security mechanisms for identity validation and access control. All permissions and resources are provisioned through customer-reviewed Infrastructure-as-Code templates to ensure transparency.

The following table maps each capability to the customer-side IAM role and the Cortex-side identity used for authentication:<br>

| Capability                                                                     | Customer account IAM role assumed | Cortex XSIAM principal that assumes the role                                                                             |
| ------------------------------------------------------------------------------ | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Discovery, ADS, Kubernetes Security, Automation, DSPM (platform-level actions) | CortexPlatformRole                | role/gcp\_saas\_role                                                                                                     |
| DSPM (data scanning)                                                           | CortexPlatformScannerRole         | role/dspm\_scanner                                                                                                       |
| Registry scanning                                                              | CortexPlatformScannerRole         | role/registry\_scanner                                                                                                   |
| Serverless scanning                                                            | CortexPlatformScannerRole         | role/scanner\_of\_serverless                                                                                             |
| Audit log collection                                                           | CloudTrailReadRole                | Cortex XSIAM log collector (via Google OIDC: accounts.google.com with a specific audience and Google service-account ID) |
