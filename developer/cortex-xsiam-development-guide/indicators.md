---
description: Cortex XSIAM guidance for indicators, relationships, and extraction.
---

# Indicators

Indicators are artifacts associated with alerts, and are an essential part of the alert management and remediation process. They help correlate alerts, create hunting operations, and enable you to easily analyze alerts and reduce Mean Time to Response (MTTR).

Cortex XSIAM includes integrations that fetch indicators from either a vendor-specific source or from a generic source, such as a CSV or JSON file.

When indicators are ingested, regardless of their source, they have a unified, common set of indicator fields, including traffic light protocol (TLP), expiration, verdict, and tags
