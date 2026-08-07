---
description: >-
  This page consolidates application security posture data across all onboarded
  instances
---

# Provider Instances Security Check

The **Provider Instances** page provides a high-level aggregation of tenant security scores and an interactive, list view for analyzing and remediating individual instances.

<img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fx9JcEbsgHuDFKPWsALgl%2Funknown.png?alt=media&#x26;token=3516186e-f6fb-4d79-b1ab-b179e6fac8b9" alt="" height="383" width="624">

\
This page consolidates SaaS application security posture data across all onboarded instances:

* Overall Security Check Score: Displays the global average posture score across all integrated instances. Applications are further categorized into three security score-based buckets:
* Up to 50% (Red): Severe posture gaps &#x20;
* Between 50%–75% (Yellow): Moderate posture alignment&#x20;
* Over 75% (Green): High posture alignment &#x20;
* Providers (Distribution Tiles): Lists onboarded SaaS Applications with active instance count for each provider.

**Instance Inventory List**

The table displays granular telemetry for each active SaaS application.&#x20;

Provider Instances: The unique, user-defined identifier/name for the specific SaaS tenant. These are hyperlinked to route administrators to the deep-dive configuration and issues page for that specific instance.

* Provider Type: The underlying third-party SaaS vendor platform associated with the instance (e.g., Mural, Cisco Meraki).
* Application Tag: Custom metadata tags assigned to instances to categorize environments for scoped policies and reporting.
* Connector Status: The operational state of the API integration. A green Connected status indicates active, authorized data ingestion.
* Overall Security Check Score: The normalized security score (0–100%) computed for the individual instance.

Click on an instance to view Passed Checks and take action on Failed Checks.
