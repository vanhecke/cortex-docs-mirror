---
description: >-
  Use Cortex XSIAM to identify externally inferred CVEs affecting
  internet-facing assets and prioritize remediation.
---

# Externally inferred CVEs

Cortex XSIAM identifies externally inferred CVEs by comparing the product name and version of an active service, if identifiable, with CVEs for those products in the National Vulnerability Database (NVD). We categorize externally inferred CVE matches as high or medium confidence based on the version information that is available on the service and from NVD.

* **High Confidence Match**—Precise version information is available both from the service and from NVD. Cortex XSIAM generates issues for high-confidence externally inferred CVEs.
* **Medium Confidence Match**—Part of the version information from the service matches the NVD entry for the CVE, but the version information from the service or from NVD has additional characters. Cortex XSIAM creates findings for medium-confidence externally inferred CVEs but will not generate issues.

{% hint style="info" %}
### Note

An externally inferred CVE might impact your service or asset, but additional investigation is required to confirm that the CVE is actually present.
{% endhint %}

The following table provides examples of externally inferred CVE matches.

| Service information available from ASM scan                                                        | CVE information available from NVD                                                                       | Match result            | Details                                                                                                                                                                                                                                                                           |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Apache v 2.4.49                                                                                    | CVE-2021-41773Affects cpe:2.3:a:apache:http\_server:2.4.49:\*:\*:\*:\*:\*:\*:\*                          | High Confidence Match   | Because the CPE information from NVD matches the version of Apache indicated from the scan, this is a high confidence match.                                                                                                                                                      |
| Apache v 2.4.49c                                                                                   | CVE-2021-41773Affects cpe:2.3:a:apache:http\_server:2.4.49:\*:\*:\*:\*:\*:\*:\*                          | Medium Confidence Match | Because the version numbers from the service and the NVD information match, except for the additional character in the version from the service, this is a medium confidence match.                                                                                               |
| Apache v 2.4.50                                                                                    | CVE-2021-41773Affects cpe:2.3:a:apache:http\_server:2.4.49:\*:\*:\*:\*:\*:\*:\*                          | No Match                | Because the CPE information from NVD indicates a version of Apache that is different than the one we saw in the scan, this does not match.                                                                                                                                        |
| Apache v 2.4.50 (Running on Red Hat Enterprise Linux 6 (RHEL6), which is not affected by this CVE) | CVE-2022-22719Affects cpe:2.3:a:apache:http\_server:\*:\*:\*:\*:\*:\*:\*:\* (up to and including 2.4.52) | High Confidence Match   | Because the CPE information from NVD matches the version of apache indicated from the scan, this is a high confidence match. Cortex XSIAM cannot determine if mitigating controls are in place or the underlying OS, so this pairing will still generate a high confidence match. |
| Apache (any version number)                                                                        | CVE-2012-3526Affects cpe:2.3:a:apache:http\_server:\*:\*:\*:\*:\*:\*:\*:\*                               | No match                | Because this CVE does not indicate any specific version number, we do not consider it a match for any version of Apache http\_server, regardless of version information.                                                                                                          |
