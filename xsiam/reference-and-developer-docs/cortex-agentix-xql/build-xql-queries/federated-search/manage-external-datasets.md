---
description: Manage external datasets used by Federated Search in Cortex XSIAM.
---

# Manage external datasets

Manage external datasets created for federates searches in **Settings → Configurations → Data Management → Dataset management → External Datasets**.

On this page you can do the following:

* Add an external dataset: Click **Add External Dataset**.
* Check the connection status: The connection status is automatically checked once a week. To manually check the connection status, hover to the right on the dataset row and click **Check connection**.
* View: Hover to the right on the dataset row and click the eye icon.
*   Edit: This opens the setup wizard where you can change the description and the schema.

    <div data-gb-custom-block data-tag="hint" data-style="success" class="hint hint-success"><p><strong>NOTE:</strong></p><p>We highly recommend that you don't change the auto-detected schema. However, in the <strong>Edit</strong> window you can add new fields or delete the new fields you added in the <strong>Edit</strong> window. You can't delete the fields that were configured during setup.</p></div>
*   Delete the dataset: Hover to the right on the dataset row and click **Delete dataset**.

    This action deletes the dataset connection in Cortex XSIAM. The dataset in your external storage isn't affected.
* Run a query using the dataset: Hover to the right on the dataset row and click the triangle. This opens the Query Builder page, with the dataset already defined.
