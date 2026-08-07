# Manage Kubernetes Connector instances

1. Navigate to Settings → Data Sources & Integrations.
2. Find the Kubernetes instance by clicking on the Kubernetes name or using the **Search** field.
3. In the row for the Kubernetes instance, click **View Details**. The **Kubernetes Connectors** page is displayed with all deployed Kubernetes Connectors. To view all Kubernetes clusters, including ones that are not yet deployed, go to the **Kubernetes Connectivity Management** page.
4. In the **Kubernetes Connectors** page, click on a cluster name to open the details pane for that instance.
5.  You can perform the following actions on each Kubernetes Connector instance:

    | Action               | Instructions                                                                                                                                                                                                                                                                                                                                                                                                          |
    | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Open Cluster Details | In the details pane, click the more options icon and select **Open Cluster Details**. The Asset Card for that Kubernetes cluster is displayed.                                                                                                                                                                                                                                                                        |
    | Edit Connector       | In the row for the Kubernetes instance, right-click and select **Edit**. Alternatively, in the details pane, click the more options icon and select **Edit Connector**. In **Edit Kubernetes Connector**, edit the configurations and click **Apply Changes**.You must execute the updated template in the Kubernetes environment for the configuration changes to be applied.                                        |
    | Delete Connector     | In the row for the Kubernetes instance, right-click and select **Delete**. Alternatively, in the details pane, click the more options icon and select **Delete Connector**. To remove the connector, you must manually run Kubernetes commands to delete the resources in the Kubernetes environment. The commands are listed [here](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete). |

**Kubernetes Connectivity Management**

Navigate to **Settings** → **Data Sources & Integrations** and find the Kubernetes instances by clicking on the Kubernetes name or using the **Search** field. In the **Kubernetes Connectors** page, click **Kubernetes Connectivity Management** to view all detected Kubernetes clusters. Here, you can check if a cluster is connected, view the status, and see the connector version. When a new version of the Kubernetes Connector is available, you can update it here.

{% hint style="info" %}
### Note

After uninstalling the Kubernetes connector, the connector status updates to Not connected 48 hours after the uninstall process is initiated.
{% endhint %}
