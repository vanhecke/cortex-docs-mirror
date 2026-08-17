---
description: Access and update issue and case context data in playbooks.
---

# Use context data in a playbook

In Cortex XSIAM you can use context data (from an issue or case) in playbooks, and you can use playbook tasks to update context data. You can:

* Use the information stored in the issue context data as task inputs and outputs in a playbook.
  *   To access data that is stored in the issue context data, use the keyword `issue`.

      Example:

      To access the `status` value in the issue context data, use the following syntax:

      ```programlisting
      ${issue.status}
      ```
  *   To access data that is stored in the parent case context data, use the keyword `parentIncidentContext`.

      Example:

      To access the `hostname` value in the case context data, use the following syntax:

      ```programlisting
      ${parentIncidentContext.hostname}
      ```
*   Set a breakpoint in a playbook that reviews context data after a specific task.

    This is available when using the debugger. As context data may be updated during a playbook run, setting a breakpoint enables you to pause the playbook execution, review the context data, and take action if necessary. Breakpoints can be useful when designing and troubleshooting playbooks. For more information, see [Test your playbook](../playbooks/build-your-playbook/test-your-playbook).
*   Add a task that writes playbook data to the case context.

    When you add data to the case context, you can use this data to run playbooks on any of the issues that are included in the case.

    To write playbook data to the case context, use the `setParentIncidentContext` script in a standard task. For more information, see [Add context data to a case](add-context-data-to-a-case).

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Users with Trigger Playbook permissions on a given issue may still be able to modify the parent case via commands and scripts, even without full access to the case.</p></div>

For more information about playbooks, see [Playbooks overview](../playbooks/playbooks-overview).

**Context data in sub-playbooks**

By default, the context data for sub-playbooks is stored in a separate context key. Consider the following information:

* When a task in a main playbook accesses context data, it does not have direct access to sub-playbook data.
* When a task in a sub-playbook accesses context data, it does not have direct access to the main playbook data.
* If the sub-playbook has been configured to share globally, the sub-playbook context data is available to the main playbook and vice versa.

{% hint style="info" %}
Generic polling does not work if a playbook’s context data is shared globally. For more information, see [Playbook polling](https://app.gitbook.com/s/1BTuP6WlLsNzo2wlKa5w/customize-cortex-xsoar/customize-and-configure-cortex-xsoar/playbooks/playbook-polling).
{% endhint %}

**Use case: Use context data in a Jira ticketing system**

In this use case, a Jira ticketing system is used to manage issues and reduce duplicate tickets.

**Issue:** When an action is taken on an endpoint, some cases contain multiple issues for the same endpoint. If each issue runs a playbook on the same endpoint, duplicate tickets are created for each case.

**Solution:** This playbook checks existing endpoints and Case IDs and decides whether to create a new ticket or to add the data to an existing ticket, and therefore, reduces duplicate tickets in the case.

![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-6890cdc9dff58267f3ab1c8aec2f3ee5ddac67ce%2F40124db1498b5fd0c1eece239d4a1edca0dc1ab5266bb420648fa4ea6019d46b.png?alt=media)

The playbook flow is described in the following steps:

1.  After checking that the Jira v3 integration is enabled, in this task the playbook adds the `EndpointFromAlerts` key to the case context by retrieving the `alert.hostname` and using the `setParentIncidentContext` script.

    ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-71f1ba05be596103dff8e0fe300bf973d138d7a1%2F32a1c76050bca0dcd30a3816641f11aa0be89861fd9c6aa8fc1ee21dcd7a9dc8.png?alt=media)
2.  In this task, the playbook checks if there is an open ticket for the case by retrieving the `parentIncidentContext.TicketID`.

    ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-4810cf3f15116edd2ae9add7f399f6e64b6997b1%2Fce69b7ab0c672e5abd35dec55dea9b6b2b8c5d6f2ac10568a9f379e68362981d.png?alt=media)
3.  If there is no open ticket, a new ticket is created in Jira and the TicketID is added to the case context.

    ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-65b0c21bb12e897c8991a96766fafd756a9d646b%2F7f674a2d336e611aa5e5be825eb39356aa17a576613e32eea3160163d9fdbd62.png?alt=media)
4.  If there is an open ticket, this task checks whether there is an open ticket for the endpoint by comparing the `alert.hostname` (issue endpoint) to the `parentIncidentContent.EndpointFromAlerts` key.

    ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-3a6156b705d942105294f43619de0fcd81c726d3%2F3d8dd1152fa89ac90e4df0c8799fd3d772e3ddfb796e32085e74bb6837de1972.png?alt=media)
5.  After retrieving the `alert.hostname` in the `parentIncidentContext.EndpointFromAlerts` context, if there is no open ticket for the endpoint, the playbook updates the Jira ticket for the case.

    In this example, you can see that the `EndpointFromAlerts` and `TicketID` has been added to the case context data.

    ![](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-db22c46a22c5ed4bc7b2cb6fbb515ccd373c6764%2F3d9a716e2fb987e19e06ed11b6eae3dd86f553e427e1f47312432760520d35c6.png?alt=media)
