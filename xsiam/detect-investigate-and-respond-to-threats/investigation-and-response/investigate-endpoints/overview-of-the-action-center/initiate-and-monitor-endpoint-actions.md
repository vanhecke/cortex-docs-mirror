# Initiate and monitor endpoint actions

In the **Action Center** you can initiate and monitor actions on your endpoints. In addition, you can initiate endpoint actions when viewing details about an endpoint on the **All Endpoints** page.

<details>

<summary>Initiate an endpoint action from the Action Center</summary>

Create new administrative actions using the **Action Center** wizard:

1. Go to **Investigation & Response → Response → Action Center →** **New Action**.
2.  Select the action you want to initiate and follow the required steps and parameters you need to define for each action.

    Cortex XSIAM displays only the endpoints eligible for the action you want to perform.
3.  Review the action summary and click **Done**.

    Cortex XSIAM will inform you if any of the agents in your action scope will be skipped.
4.  Track your action.

    Track the new action in the **Action Center**. The action status is updated according to the action progress.

</details>

<details>

<summary>Monitor endpoint actions</summary>

1. Go to **Investigation & Response → Response** → **Action Center**.
2. Select the relevant view from the left-side menu on the **Action Center** page.
3. Use the table filters to filter the results.
4. Take further actions. Right-click the action to see the available options:
   * **Additional data:** Display additional details for the action, such as file paths for quarantined files or operating systems for agent upgrades. For actions with **Status**, **Failed** or **Completed with partial success**, you can create an upgrade action to rerun the action on endpoints that have not been completed successfully.
   * **Archive:** Archive the action for future reference. You can select multiple actions to archive at the same time.
   * **Cancel for Pending endpoints:** Cancel the original action for agents that are still in `Pending` status.
   * **Download output:** Download a zip file with the files received from the endpoint for actions such as file and data retrieval.
   * **Rerun:** Launch the **Define an Action** wizard populated with the same details as the original action.
   * **Run on additional agents:** Launch the action wizard populated with the details as the original action except for the agents which you have to fill in.
   * **Restore:** Restore quarantined files.

</details>
