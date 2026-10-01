---
description: >-
  Learn more about technical conventions for complex network scenarios in Cortex
  XSIAM.
---

# Advanced network mapping: deep dives

This section provides technical conventions for complex network scenarios, including how to handle asymmetric flows and vendor-specific logging dialects.

### Implementation order of operations

1. **MAP**: Directly use the source field if it carries the value.
2. **DERIVE**: Construct the value from other fields (e.g., deriving `is_internal_ip` from the IPv4).
3. **PAD**: Use semantically empty placeholders only if derivation is impossible. Never pad a specific protocol (like `TCP`) if you aren't certain.

### Topology and identity

* **Directionality**: Invert topology is a common error. Always confirm which end initiated the flow. A device logging traffic _through_ itself is the `xdm.observer`, while the endpoints are the `source` and `target`.
* **Double-logging**: Some products (e.g., OS and Application layers) log one session twice. Model both, but note this in the dataset metadata so analytical queries can deduplicate on session IDs.

### Vendor-specific modeling rules

#### FortiGate Native Key=Value

FortiOS emits native logs where field names like `srcip`, `sentbyte`, and `rcvdbyte` do not overlap with CEF formats.

* **Action vocabulary**: FortiGate actions like `timeout` or `server-rst` should map to `OUTCOME_SUCCESS` (policy permitted) rather than `FAILED`.
* **Observer ID**: The `devid` is the appliance serial number and belongs in `xdm.observer.unique_identifier`, not the client device ID.

#### Cisco IOS-XE Mnemonics

* **ACL logging**: Mnemonics like `SEC-6-IPACCESSLOGP` indicate which fields (ports, protocols) are present. Use these suffixes to determine which fields can be mapped vs. padded.
* **Firewall findings**: Records like `FW-5-IMAP_NON_SECURE_LOGIN` are cleartext credential exposures. Map these as network flows first and treat the captured text as an alert.
