# Isolate an endpoint

When you isolate an endpoint, you halt all network access on the endpoint except for traffic to Cortex XSIAM. This can prevent a compromised endpoint from communicating with other endpoints, thereby reducing an attacker’s mobility on your network. After the agent receives the instruction to isolate the endpoint and carries out the action, Cortex XSIAM shows an **Isolated** status. To ensure an endpoint remains in isolation, agent upgrades are not available for isolated endpoints.

When isolated, the endpoint will still allow:

* DHCP and HTTPS outgoing traffic for root user
* DNS traffic

{% hint style="info" %}
IP-based file storage protocol traffic will also be blocked. This might affect endpoint functionality if the endpoint uses such mounts.
{% endhint %}

Network isolation is supported for endpoints that meet the following requirements:

<table><thead><tr><th width="121">Operating System</th><th>Prerequisites</th></tr></thead><tbody><tr><td>Windows</td><td><ul><li>Agent 6.0 or later.</li><li>(VDI) Network isolation allow list in the agent settings profile is configured to ensure VDI sessions remain uninterrupted. For more information, see Set up agent settings profiles.</li></ul></td></tr><tr><td>Mac</td><td><ul><li>Agent 7.3 or later.</li><li>MacOS 10.15.4 or later.</li><li>Cortex XSIAM Network extension is enabled on the endpoint.</li></ul><p>Network isolation on Mac endpoints does not terminate active connections that were initiated before the agent was installed on the endpoint.</p></td></tr><tr><td>Linux</td><td><ul><li>iptables and ip6tables.</li><li>Agent 7.7 or later.</li><li><p>Linux kernel with the following enabled:</p><ul><li>CONFIG_NETFILTER</li><li>CONFIG_IP_NF_IPTABLES</li><li>CONFIG_IP_NF_MATCH_OWNER</li></ul></li><li>Network isolation allow list configured in the agent settings profile.</li></ul><p>Network isolation on Linux endpoints is based on the defined IP addresses and ports.</p></td></tr><tr><td>iOS</td><td>Supported by Cortex XDR agent for iOS 9.1 or later. This feature is only available on supervised iOS devices where the Network Shield is enabled.</td></tr></tbody></table>

### How to isolate an endpoint

1.  Go to Investigation & Response → Response → Action Center → **New Action** and select **Isolate**.

    You can also initiate the action (for one or more endpoints) from the **Isolation** page of the **Action Center** or from Endpoints → Endpoint Management → **Endpoint Administration**.
2.  Enter a **Comment** to provide additional background or other information that explains why you isolated the endpoint.

    After you isolate an endpoint, Cortex XSIAM displays the **Isolation Comment** under Action Center → **Isolation**. If needed, you can edit the comment from the right-click pivot menu.
3. Click **Next**.
4.  Select the target endpoint that you want to isolate from your network.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>If needed, <strong>Filter</strong> the list of endpoints.</p></div>
5. Click **Next**.
6.  Review the action summary and click **Done** when finished.

    In the next heartbeat, the agent will receive the isolation request from Cortex XSIAM.
7.  To track the status of an isolation action, go to Action Center → Currently Applied Actions → **Endpoint Isolation**.

    If after initiating an isolation action, you can cancel the action by right-clicking the action and selecting **Cancel for pending endpoint**. You can cancel the isolation action only if the endpoint is still in `Pending` status and has not been isolated yet.
8.  After you remediate the endpoint, cancel endpoint isolation to resume normal communication.

    You can cancel isolation from Actions Center → Isolation or from Endpoints → Endpoint Management → **Endpoint Administration**. From either place right-click the endpoint and select Endpoint Control → **Cancel Endpoint Isolation**.

{% hint style="info" %}
If file system operations become unresponsive during isolation, such as being unable to list folder content, unmount the mounted network shares.
{% endhint %}
