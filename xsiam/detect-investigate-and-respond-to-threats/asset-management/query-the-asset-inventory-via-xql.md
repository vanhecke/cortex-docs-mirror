---
description: Query asset inventory data with XQL in Cortex XSIAM.
---

# Query the asset inventory via XQL

While the asset inventory provides extensive filtering capabilities, you may need to perform complex, programmatic searches across your environment. The entire asset inventory is available to be queried via XQL using the `asset_inventory` dataset.

For advanced identity use cases, such as Cloud Infrastructure Entitlements Management (CIEM) permissions analysis, you should use the `ciem_permissions_with_last_access` dataset. This dataset contains the permissions of each identity discovered in your environments, including the time of their last access, providing deep visibility into identities and permissions.

**Key asset fields**

When querying the `asset_inventory` dataset, Cortex XSIAM uses the normalized Cortex Data Model (XDM) schema. Here is a reference list of the most important `xdm.asset.*` fields you should know for your queries.

Identity and classification:

* **xdm.asset.id:** The unique asset identifier.
* **xdm.asset.name:** The human-readable asset name.
* **xdm.asset.type.class:** The broad asset class, such as Compute, Identity, AI, or Network.
* **xdm.asset.type.category:** The category within the class, such as Database, Storage Bucket, or Model Endpoint.
* **xdm.asset.provider:** The cloud provider (e.g., AWS, GCP, AZURE) or data source.
* **xdm.asset.realm:** The account, subscription, or project the asset belongs to.

Location and configuration:

* **xdm.cloud.region:** The cloud region (e.g., US-EAST-1).
* **xdm.cloud.zone:** The availability zone.
* **xdm.asset.normalized\_fields:** A JSON blob containing normalized, cross-provider fields.
* **xdm.asset.raw\_fields:** A JSON blob containing all of the raw, provider-specific data collected from the source.

Security context and timing:

* **xdm.asset.group\_ids:** Identifies the asset's group memberships (used for SBAC scoping).
* **xdm.asset.issues\_critical / xdm.asset.cases\_critical:** The count of critical issues or cases linked to this asset.
* **xdm.asset.first\_observed / xdm.asset.last\_observed:** Timestamps indicating when the asset was first and last seen by Cortex XSIAM.

**Asset query examples**

The following are examples of how to combine the `asset_inventory` dataset with the key XDM fields to find specific resources.

**Find all AWS Compute Instances:**

```
dataset = asset_inventory| filter xdm.asset.provider = "AWS" AND xdm.asset.type.class = "Compute"
```

**Find assets in a specific cloud region:**

```
dataset = asset_inventory| filter xdm.cloud.region = "US-EAST-1"
```

**Search for specific database assets by name:**

```
dataset = asset_inventory| filter xdm.asset.name contains "prod-db"| limit 10
```
