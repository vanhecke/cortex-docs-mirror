---
description: >-
  Learn more about technical conventions and implementation logic for complex
  authentication scenarios in Cortex XSIAM.
---

# Authentication mapping: Advanced classification and deep dives

This section provides technical conventions and implementation logic for complex authentication scenarios. Use this guide to ensure that identity classification and entity relationships are modeled correctly for the identity analytics engine.

### Standard implementation rules

When a mandatory field is missing from your source log, apply these treatments in order. Padding is the LAST resort and should only be used when the information is truly unavailable and cannot be constructed.

1. **MAP**: Directly use the source field if it carries the required value.
2. **DERIVE**: Construct the value from other available fields.
   * **UPN construction**: For device-local accounts without a domain, synthesize the UPN using the `<account>@localhost` convention.
   * **Privilege banding**: Map numeric vendor levels to XDM constants (such as TACACS+ Level 15+ maps to `XDM_CONST.PRIVILEGE_LEVEL_ADMIN`).
3. **PAD**: Use semantically empty placeholders only if derivation is impossible.
   * **Permitted**: `to_integer(0)` for ports, `""` for target IP, and `XDM_CONST.IP_PROTOCOL_IP` for transport.
   * **Prohibited**: Never pad `xdm.target.resource.name` or `xdm.source.ipv4`. If the target is unknown, let the field resolve to null.

### Technical modeling by log family

#### Windows logon and Kerberos

* **Entity mapping**: `TargetUserName` and `TargetDomainName` represent the source user. `IpAddress` and `IpPort` represent the source endpoint.
* **Logon types**: Map Windows numeric LogonTypes to the corresponding `xdm.logon.type` constants (such as, 2 to `INTERACTIVE`, 3 to `NETWORK`).
* **Kerberos details**: Map encryption types and Status hex codes to the appropriate `xdm.auth.kerberos_*` sub-fields.

#### AAA Gateways (TACACS+, RADIUS, Cisco ISE)

These logs involve a **three-party topology** that must be modeled accurately:

* **Principal**: The user being authenticated (`xdm.source.user.upn`).
* **Source**: The IP of the user's physical workstation (`xdm.source.ipv4`).
* **Target**: The network device or console being managed (`xdm.target.ipv4` and `xdm.target.resource.name`).

#### Cisco Wireless (WLC)

* **Population differentiation**: WLC distinguishes between administrative operators and wireless network clients. These must be mapped to distinct `xdm.source.user.user_type` values to ensure management activity is not merged with client traffic.
* **Security enforcement signals**: Critical records such as `CLIENT_SHUNNED` or `SECURITY_VIOLATION` represent active enforcements and must be included in the authentication story, regardless of their raw severity level.
