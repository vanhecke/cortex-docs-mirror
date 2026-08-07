# Manage agent tokens

You can now run some of the agent functions that require administrative passwords using a unique token shared between Cortex XSIAM and Cortex XDR agent.

Two types of tokens can be set:

* **Rolling token:** Automatically generated per endpoint every fourteen days by the system and then sent to the relevant agent
* **Temporary token:** Set a temporary token that is valid anywhere from one to twenty-one days.

{% hint style="info" %}
**Note:**

Agent tokens are only supported for Windows and Mac.
{% endhint %}

{% stepper %}
{% step %}
#### View agent password

You can view the password of the selected agent. The dialog box indicates whether the password is from a rolling token or a temporary token.

1. Select Inventory → Endpoints → All Endpoints → Endpoint Control → View Token.
2. Click the copy button to copy the password displayed and then click OK.

You can now use the password to run functions at the agent.
{% endstep %}

{% step %}
#### Add a temporary token

You can generate a temporary token for any of the agents for a specified number of days between 1 and 21 days. If the agent is disconnected, it gets the temporary token when the agent connects.

{% hint style="info" %}
**Note:**

You can select one or multiple agents to add a temporary token.
{% endhint %}

1. Select Inventory → Endpoints → All Endpoints → Endpoint Control → Set Temporary Token.
2. In the Token Expiration field, add the number of days for which to generate a temporary token for the agent, and then click the Add Token Expiration blue arrow.
3. Click the copy button to copy the password displayed and then click Create to begin generating the token.
4. Go to the Action Center to view which agent received the temporary token.

You can now use the password to run functions on the agent.
{% endstep %}

{% step %}
#### Retrieve the token using the token hash from the endpoint

If the endpoint is disconnected from the server at the point the rolling token was updated, it won’t be possible to run agent functions with the updated token from the server. You can still retrieve the password to run functions on the agent.

1. From the agent, run the `cytool.exe` to run the token query command. This command displays the current token of the endpoint.
2. Copy the token from the command line interface of the agent.
3. In the server, at the top of the page, click Retrieve Token.
4. In the Retrieve Token dialog box, in the Hash field, paste the token that you copied from the endpoint.
5. Click the copy button to copy the password displayed and then click OK.

You can now use the password to run functions on the agent.
{% endstep %}
{% endstepper %}
