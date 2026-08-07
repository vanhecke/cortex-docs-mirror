# Configure a sub-playbook loop

Looping uses sub-playbooks to create loops within the main playbook. When running the loop, the values are calculated based on the context data for the sub-playbook and not the main playbook.

{% hint style="info" %}
Consider the following when adding a loop:

* The maximum number of loops (default is 100). A high number of loops or a high wait time combined with a large number of issues may affect performance.
* Periodically check looping conditions to ensure they are still valid for the data set.
* If you want a sub playbook task to loop over an array passed into its input, you need to configure a loop. Otherwise it takes in the whole array and runs once.
{% endhint %}

#### How to create a sub-playbook loop

1. In the Playbooks page, select the parent playbook that contains the sub-playbook task you want to run in a loop.
2.  Right click and select Edit.

    If the playbook is installed from a content pack, you need to duplicate or detach the playbook before editing.
3. Click the sub-playbook for which you want to create the loop.
4. In the Task Details pane, click the Loop tab.
5. Click one of the following options to define loop settings:
   * None: (Default) The sub-playbook does not loop.
   *   Built-in: Use built-in functions to define loop settings:

       | Option          | Description                                                                                                                                                                                                                             |
       | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
       | Exit when       | Enables you to define when to exit the loop. Click {} and expand the source category. Hover over the required source and click **Filter & Transform** to the left of the source to manipulate the data.                                 |
       | Equals (String) | Select the operator to define how the values should be evaluated.                                                                                                                                                                       |
       | Max iterations  | <p>The number of times the loop should run.</p><div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Balance the number of iterations and the interval to avoid overloading the server.</p></div> |
       | Sleep           | <p>The number of seconds to wait between iterations.</p><p>recommends that you balance between the number of iterations and the number of seconds to wait between iterations so you don't overload the server.</p>                      |
   * For each input: Runs the sub-playbook based on defined inputs. Enter the number of seconds to wait between iterations.
   * Choose Loop automation: Select the automation from the drop-down list to define when to exit the loop. The parameters that appear are applicable to the selected automation.
6. To save the changes, click OK.

#### **Example: Exit looping after running for all inputs**

In the parent playbook (the task that contains the sub-playbook), you can configure to exit a loop running the sub-playbook automatically when the last item in the sub-playbook input is executed.

* If the input is a single item, the sub-playbook runs once, but if the input is a list of items (such as a list of issue IDs), the sub-playbook runs as many times as there are items in the list. Each iteration of the sub-playbook uses the next item in the list as the input.
* If there are multiple input lists with the same number of items, the sub-playbook runs once for each set of inputs.
*   If there are multiple input lists with different amounts of items, the sub-playbook runs the first set of inputs, followed by the second, third, and so on, until the end.

    For example:

    | Input   | Value   |
    | ------- | ------- |
    | Input x | 1,2,3,4 |
    | Input y | a,b,c,d |
    | Input z | 9       |

    The first loop: 1, a, 9

    The second loop: 2, b, 9

    The third loop: 3, c, 9

    The fourth loop: 4, d, 9
