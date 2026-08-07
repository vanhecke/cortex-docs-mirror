# Serverless runtime issues

You can view all serverless function issues detected by an agent and generated from policy violations under **Issues** (under Cases & Issues) inventories.

Every policy violation creates an issue per type:

* Process activity - enables specifying specific allowed list processes, blocking all processes except the main process and detecting crypto mining attempts.
* Network activity - enables monitoring and enforcement of DNS resolutions, inbound and outbound network connections.
* Filesystem activity - enables defining specific paths in an allowed or denied list.

Additional issues from specific policy violation are raised, which include the same cloud provider, region, runtime, function name, function version, issue name and issue description, will be suppressed.

The **Issues** page includes the following information indicating unique serverless function issues raised by agents:

| Field                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain                    | For serverless, this is set to **Security**.                                                                                                                                                                                                                                                                                                                                                                                                              |
| Category                  | For serverless, this is set to **Cloud**.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Name                      | <p>For serverless, the relevant issue name appears:</p><ul><li>Serverless function Network Policy violation for outbound ports</li><li>Serverless function Network Policy violation for listening ports</li><li>Serverless function Network Policy violation for DNS</li><li>Serverless function Network Policy violation for IPs</li><li>Serverless function File system Policy violation</li><li>Serverless function Process Policy violation</li></ul> |
| Detection method          | For serverless, this is set to **XDR agent**.                                                                                                                                                                                                                                                                                                                                                                                                             |
| Severity                  | For serverless, this is always set to **High**.                                                                                                                                                                                                                                                                                                                                                                                                           |
| Cloud Function Runtime    | <ul><li>Python</li><li>Node.JS</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Cloud Function Request ID | Instance id from the cloud provider.                                                                                                                                                                                                                                                                                                                                                                                                                      |

{% hint style="info" %}
### Note

Issues triggered within 24 hours, sharing the same name and description, will be aggregated into cases along with issues from the same function per execution.
{% endhint %}
