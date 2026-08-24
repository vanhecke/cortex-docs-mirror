---
description: Review event forwarding fields by Cortex XSIAM event type.
---

# Endpoints Event Forwarding - included/excluded fields by event type

{% hint style="warning" %}
### Prerequisite

Event Forwarding requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Dataset Management.
{% endhint %}

Endpoints Event Forwarding exports raw, high-fidelity security telemetry collected by EDR, including data from endpoints through the XDR Agent and cloud workloads (VMs, containers, or third-party EDRs). The exported logs are raw data, without any stories, and export a subset of the endpoint data without filtering or configuration options.

<details>

<summary>Types of events exported for the endpoints</summary>

The table below lists the types of events exported for the endpoints and the fields that are included and excluded:

#### Exported event type: Network

| Included field                   | Excluded field                |
| -------------------------------- | ----------------------------- |
| action\_socket\_type             | is\_boot\_replay              |
| action\_remote\_ip               | action\_proxy                 |
| action\_remote\_port             | action\_network\_app\_ids     |
| action\_local\_ip                | action\_network\_rule\_ids    |
| action\_local\_port              | action\_network\_dpi\_fields  |
| action\_network\_connection\_id  | action\_network\_is\_loopback |
| action\_network\_is\_server      | action\_upload                |
| action\_network\_creation\_time  | action\_download              |
| action\_total\_upload            | action\_network\_stats\_seq   |
| action\_total\_download          | action\_network\_is\_ipv6     |
| action\_network\_protocol        |                               |
| action\_network\_stats\_is\_last |                               |

#### Exported event type: Process

| Included field                             | Excluded field                                 |
| ------------------------------------------ | ---------------------------------------------- |
| uuid / \_id                                | action\_process\_causality\_id                 |
| action\_process\_os\_pid                   | action\_process\_is\_causality\_root           |
| action\_process\_instance\_id              | action\_process\_is\_replay                    |
| action\_process\_image\_md5                | action\_process\_yara\_file\_scan\_result      |
| action\_process\_image\_sha256             | action\_process\_wf\_verdict                   |
| action\_process\_image\_path               | action\_process\_static\_analysis\_score       |
| action\_process\_image\_name               | execution\_actor\_causality\_id                |
| action\_process\_image\_extension          | action\_process\_ns\_pid                       |
| action\_process\_image\_command\_line      | action\_process\_container\_id                 |
| action\_process\_signature\_product        | action\_process\_is\_container\_root           |
| action\_process\_signature\_vendor         | action\_process\_image\_command\_line\_indices |
| action\_process\_signature\_is\_embedded   | action\_process\_is\_special                   |
| action\_process\_signature\_status         | action\_process\_ns\_user\_sid                 |
| action\_process\_integrity\_level          | action\_process\_ns\_user\_real\_sid           |
| action\_process\_username                  | action\_process\_file\_size                    |
| action\_process\_user\_sid                 | action\_process\_file\_create\_time            |
| action\_process\_in\_txn                   | action\_process\_file\_mod\_time               |
| action\_process\_pe\_load\_info            | action\_process\_remote\_session\_ip           |
| action\_process\_peb                       | action\_process\_file\_info                    |
| action\_process\_peb32                     | action\_process\_device\_info                  |
| action\_process\_last\_writer\_actor       | execution\_actor\_instance\_id                 |
| action\_process\_token                     | action\_process\_user\_real\_sid               |
| action\_process\_privileges                | action\_process\_requested\_parent\_pid        |
| action\_process\_fds                       | action\_process\_requested\_parent\_iid        |
| action\_process\_scheduled\_task\_name     |                                                |
| action\_process\_termination\_date         |                                                |
| action\_process\_instance\_execution\_time |                                                |
| action\_process\_termination\_code         |                                                |

#### Exported event type: File

| Included field                        | Excluded field                          |
| ------------------------------------- | --------------------------------------- |
| action\_file\_path                    | action\_file\_wf\_verdict               |
| action\_file\_name                    | action\_file\_yara\_file\_scan\_result  |
| action\_file\_previous\_file\_path    | action\_file\_dir\_query                |
| action\_file\_previous\_file\_name    | action\_file\_previous\_device\_info    |
| action\_file\_md5                     | action\_file\_device\_info              |
| action\_file\_sha256                  | action\_file\_reparse\_path             |
| action\_file\_size                    | action\_file\_reparse\_count            |
| action\_file\_attributes              | action\_file\_dirty\_reason             |
| action\_file\_create\_time            | action\_file\_remote\_ip                |
| action\_file\_mod\_time               | action\_file\_remote\_port              |
| action\_file\_access\_time            | action\_file\_remote\_file\_ip          |
| action\_file\_type                    | action\_file\_remote\_file\_host        |
| action\_file\_operation\_flags        | action\_file\_sec\_desc                 |
| action\_file\_mode                    | action\_file\_previous\_file\_extension |
| action\_file\_owner                   | action\_file\_extension                 |
| action\_file\_owner\_name             | action\_file\_archive\_list             |
| action\_file\_group                   | action\_file\_contents                  |
| action\_file\_group\_name             |                                         |
| action\_file\_device\_type            |                                         |
| action\_file\_signature\_product      |                                         |
| action\_file\_signature\_vendor       |                                         |
| action\_file\_signature\_is\_embedded |                                         |
| action\_file\_signature\_status       |                                         |
| action\_file\_pe\_info                |                                         |
| action\_file\_prev\_type              |                                         |
| action\_file\_last\_writer\_actor     |                                         |
| action\_file\_is\_anonymous           |                                         |

#### Exported event type: Registry

| Included field                   | Excluded field |
| -------------------------------- | -------------- |
| action\_registry\_value\_type    |                |
| action\_registry\_key\_name      |                |
| action\_registry\_data           |                |
| action\_registry\_value\_name    |                |
| action\_registry\_old\_key\_name |                |
| action\_registry\_file\_path     |                |
| action\_registry\_return\_val    |                |

#### Exported event type: Injection

| Included field                                   | Excluded field                                         |
| ------------------------------------------------ | ------------------------------------------------------ |
| action\_remote\_process\_thread\_id              | action\_remote\_process\_causality\_id                 |
| action\_remote\_process\_os\_pid                 | action\_remote\_process\_is\_causality\_root           |
| action\_remote\_process\_instance\_id            | action\_remote\_process\_is\_replay                    |
| action\_remote\_process\_image\_md5              | action\_remote\_process\_image\_extension              |
| action\_remote\_process\_image\_sha256           | action\_remote\_process\_image\_command\_line\_indices |
| action\_remote\_process\_image\_path             | action\_remote\_process\_is\_special                   |
| action\_remote\_process\_image\_name             | action\_remote\_process\_file\_size                    |
| action\_remote\_process\_image\_command\_line    | action\_remote\_process\_file\_create\_time            |
| action\_remote\_process\_signature\_product      | action\_remote\_process\_file\_mod\_time               |
| action\_remote\_process\_signature\_vendor       | action\_remote\_process\_file\_info                    |
| action\_remote\_process\_signature\_is\_embedded |                                                        |
| action\_remote\_process\_signature\_status       |                                                        |
| action\_remote\_process\_thread\_start\_address  |                                                        |
| action\_remote\_process\_integrity\_level        |                                                        |
| action\_remote\_process\_username                |                                                        |
| action\_remote\_process\_user\_sid               |                                                        |
| address\_mapping                                 |                                                        |

#### Exported event type: Load Image

| Included field                          | Excluded field                           |
| --------------------------------------- | ---------------------------------------- |
| action\_module\_path                    | action\_module\_is\_replay               |
| action\_module\_md5                     | action\_module\_yara\_file\_scan\_result |
| action\_module\_sha256                  | action\_module\_file\_size               |
| action\_module\_base\_address           | action\_module\_file\_create\_time       |
| action\_module\_image\_size             | action\_module\_file\_mod\_time          |
| action\_module\_signature\_product      | action\_module\_file\_access\_time       |
| action\_module\_signature\_vendor       | action\_module\_device\_info             |
| action\_module\_signature\_is\_embedded | action\_module\_wf\_verdict              |
| action\_module\_signature\_status       |                                          |
| action\_module\_file\_info              |                                          |
| action\_module\_last\_writer\_actor     |                                          |
| action\_module\_other\_load\_location   |                                          |
| action\_module\_page\_protection        |                                          |
| action\_module\_system\_properties      |                                          |
| action\_module\_code\_integrity         |                                          |
| action\_module\_boot\_code\_integrity   |                                          |

#### Exported event type: User Status Change

| Included field                   | Excluded field |
| -------------------------------- | -------------- |
| action\_user\_status             |                |
| action\_username                 |                |
| action\_user\_status\_sid        |                |
| action\_user\_session\_id        |                |
| action\_user\_is\_local\_session |                |

#### Exported event type: Host Status Change

| Included field       | Excluded field |
| -------------------- | -------------- |
| action\_boot\_time   |                |
| action\_powered\_off |                |

#### Exported event type: Agent Status Change

| Included field           | Excluded field                            |
| ------------------------ | ----------------------------------------- |
|                          | action\_boot\_instance\_cleanup\_required |
| agent\_status\_component |                                           |

#### Exported event type: Host Metadata Discovery/Change

| Included field                 | Excluded field |
| ------------------------------ | -------------- |
| host\_metadata\_interface\_map |                |
| host\_metadata\_hostname       |                |
| host\_metadata\_domain         |                |

</details>

<details>

<summary>Common fields for all event types</summary>

The table below lists the common fields for all event types and the fields that are included and excluded.

| Common fields for all event types | Included field                        | Excluded field                          |
| --------------------------------- | ------------------------------------- | --------------------------------------- |
| **Agent**                         | agent\_content\_version               | agent\_install\_type                    |
|                                   | agent\_hostname                       | event\_utc\_diff\_minutes               |
|                                   | agent\_interface\_map                 | manifest\_file\_version                 |
|                                   | agent\_os\_sub\_type                  | source\_message\_id                     |
|                                   | agent\_os\_type                       | zip\_id                                 |
|                                   | agent\_version                        | agent\_request\_time                    |
|                                   | agent\_id                             | server\_request\_time                   |
|                                   | agent\_ip\_addresses                  | agent\_id\_hash                         |
|                                   | agent\_ip\_addresses\_v6              | agent\_id\_hash\_bre                    |
|                                   |                                       | backtrace\_identities                   |
|                                   |                                       | \_product                               |
|                                   |                                       | \_vendor                                |
|                                   |                                       | actor\_fields                           |
|                                   |                                       | agent\_is\_vdi                          |
| **Common**                        | event\_version                        | event\_is\_impersonated                 |
|                                   | event\_type                           | event\_is\_replay                       |
|                                   | event\_sub\_type                      | event\_impersonation\_status            |
|                                   | event\_id                             | event\_is\_simulated                    |
|                                   | event\_timestamp                      | event\_user\_presence                   |
|                                   | event\_rpc\_interface\_uuid           | agent\_host\_boot\_time                 |
|                                   | event\_rpc\_func\_opnum               | agent\_session\_start\_time             |
|                                   |                                       | event\_validity\_enum                   |
|                                   |                                       | event\_invalidity\_field                |
|                                   |                                       | event\_rpc\_inteface\_version\_major    |
|                                   |                                       | event\_rpc\_inteface\_version\_minor    |
|                                   |                                       | event\_rpc\_protocol                    |
|                                   |                                       | event\_address\_mapped                  |
|                                   |                                       | event\_user\_presence\_status           |
| **Actor**                         | os\_actor\_local\_ip                  | actor\_ns\_user\_sid                    |
|                                   | os\_actor\_local\_port                | actor\_process\_auth\_id                |
|                                   | os\_actor\_primary\_user\_sid         | actor\_process\_causality\_id           |
|                                   | os\_actor\_primary\_username          | actor\_process\_ns\_pid                 |
|                                   | os\_actor\_process\_command\_line     | actor\_process\_session\_id             |
|                                   | os\_actor\_process\_image\_md5        | actor\_process\_signature\_is\_embedded |
|                                   | os\_actor\_process\_image\_name       | actor\_process\_signature\_product      |
|                                   | os\_actor\_process\_image\_path       | actor\_process\_signature\_vendor       |
|                                   | os\_actor\_process\_image\_sha256     | actor\_remote\_host                     |
|                                   | os\_actor\_process\_signature\_status | actor\_remote\_pipe\_name               |
|                                   | os\_actor\_process\_logon\_id         | actor\_remote\_port                     |
|                                   | os\_actor\_process\_os\_pid           | actor\_rpc\_interface\_version\_major   |
|                                   | os\_actor\_remote\_ip                 | actor\_rpc\_interface\_version\_minor   |
|                                   | os\_actor\_process\_instance\_id      | actor\_rpc\_protocol                    |
|                                   | os\_actor\_thread\_thread\_id         | actor\_type                             |
|                                   |                                       | actor\_rpc\_func\_opnum                 |
|                                   |                                       | actor\_rpc\_interface\_uuid             |
|                                   |                                       | actor\_process\_device\_info            |
|                                   |                                       | actor\_process\_execution\_time         |
|                                   |                                       | actor\_process\_file\_create\_time      |
|                                   |                                       | actor\_process\_file\_mod\_time         |
|                                   |                                       | actor\_process\_file\_size              |
|                                   |                                       | actor\_process\_image\_extension        |
|                                   |                                       | actor\_process\_instance\_id            |
|                                   |                                       | actor\_process\_command\_line\_indices  |
|                                   |                                       | actor\_process\_integrity\_level        |
|                                   |                                       | actor\_process\_is\_special             |
|                                   |                                       | actor\_process\_last\_writer\_actor     |
|                                   |                                       | actor\_process\_instance\_id            |
|                                   |                                       | actor\_thread\_thread\_id               |
|                                   |                                       | actor\_is\_injected\_thread             |
|                                   |                                       | actor\_causality\_id                    |
|                                   |                                       | actor\_effective\_username              |
|                                   |                                       | actor\_effective\_user\_sid             |

</details>
