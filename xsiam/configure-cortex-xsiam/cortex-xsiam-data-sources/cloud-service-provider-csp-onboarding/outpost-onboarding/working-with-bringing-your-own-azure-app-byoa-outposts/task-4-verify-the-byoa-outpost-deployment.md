---
description: >-
  You can customize your own Azure outpost by bringing your own app (BYOA). This
  page describes the steps for verifying your BYOA outpost deployment.
---

# Task 4: Verify the BYOA outpost deployment

This page lists the checks necessary for verifying that deployment is valid.

After running the Terraform and it completes successfully:

* **Check FICs**: In the Azure Portal, go to your **App Registration → Certificates & secrets → Federated credentials**. You should see federated identity credentials created by Cortex.
* **Check Cortex XSIAM**: The outpost should appear in the Cortex XSIAM console with status **Connected**.
* **Check scanning**: Cortex begins discovery and scanning after Azure has been onboarded. Confirm that the first scan starts automatically after deployment. The initial scan may take some time to begin. If no scan has started after a reasonable interval, you might need to re-download the outpost Terraform files and try again.

## What's next?

Continue with [Cortex XSIAM CSP onboarding](../../outpost-creation-workflow#phase-4-onboarding-the-csp).
