---
description: Integration parameter types that are configurable in integration instances.
---

# Integration Parameters

Each integration has parameters that are configured by the customers when they configure an instance on their Cortex XSIAM system. Integration parameters should be named using [snake\_case](https://en.wikipedia.org/wiki/Snake_case).

<details>

<summary>Supported Parameter Types</summary>

* Short text (type 0)
* Encrypted (type 4)
* Boolean Checkbox (type 8)
* Credentials (type 9)
* Long text (type 12)
* Single select (type 15)
* Multi-select (type 16)

</details>

<details>

<summary>Connection and Authentication Parameters</summary>

These parameters determine how Cortex XSIAM connects to the third-party API.

*   url

    The URL Cortex XSIAM should connect to. Always expose this parameter even in SaaS applications, as SaaS applications can have variations as well (tenant name or federal cloud, for example).
*   api\_key

    In most cases, credentials are needed to authenticate to the API you want to interact with. Many times this is in the form of an API key, a secure and unique identifier that is stored in Cortex XSIAM and used somewhere in your code (i.e. to populate HTTP headers) to craft the requests. Sometimes APIs use different authentication parameters: credentials, tokens, client\_id and client\_secret combination, and so on. Capture all the required parameters that allow a machine-to-machine authentication between Cortex XSIAM and your API.

{% hint style="info" %}
### Note

If you are using authentication mechanisms based on short-lived access tokens such as JSON Web Tokens (JWT) and long-lived refresh tokens, read more about the [Integration cache](../advanced-topics/integration-cache).
{% endhint %}

*   proxy

    Boolean to determine whether to use the system proxy setting. You don't need to handle proxy settings in your code, but you should set environment variables accordingly based on this Boolean.
*   insecure

    Boolean to determine whether to avoid verifying SSL certificates.

</details>

<details>

<summary>Event collector parameters</summary>

If your integration fetches events, you should define what type of entities in the third-party product you are connecting to and are retrieving. Every product has its own nomenclature: they might be called Alerts, Incidents, etc. For the purposes of this topic, we assume they are called Alerts in the third-party product, and they are mapped 1:1 to Cortex XSIAM alerts.

Many products are very verbose, and have the potential to generate many alerts of different types, with different levels of severity. Each alert could have a status (i.e. open or resolved) as well as attributes. SOC analysts might be interested only in a subset of the incoming Alerts. When they configure your integration in Cortex XSIAM, they expect to find parameters that allow them to filter and determine which alerts should generate incidents and which alerts should be discarded.

Common filters for fetching incidents include:

*   Maximum number of alerts per fetch

    The parameter name must be `max_fetch`. It is a good practice to limit the number of incidents you retrieve every time you fetch, in order to avoid overloading Cortex XSIAM by running many playbooks at the same time. Customers should be allowed to set this value as an integration parameter. Recommended default is 10 to 20, with a maximum of 50.
*   Severity

    Many SOCs prefer to retrieve only incidents with specific severities, from third-party systems, and to avoid importing lower severity ones incidents. The integration settings should allow customers to choose the severity of the incidents they want to retrieve. This can be done either using a multi-select, or a single-select where they specify the lowest severity level they want to retrieve.
*   Type

    Third-party products typically generate different types of alerts/events/issues/incidents. Often SOCs are interested only in a specific subset of types they want to handle automatically through Cortex XSIAM. This integration setting allows end users to specify which types of alerts they want to fetch from the third-party platform. If the types are of finite and known cardinality, we recommend using a multi-select. If the types are not known up front or may change over time, we recommend using a comma-separated text input, with a link in the details to your product documentation where an up-to-date list of those types is available.
*   First fetch

    The parameter name must be `first_fetch`. When customers configure the integration for the first time, they usually want to retrieve incidents that happened in the past. This common setting is used to specify how far back in time they want to retrieve incidents the first time the integration runs. You can check the [HelloWorld](https://github.com/demisto/content/blob/master/Packs/HelloWorld/Integrations/HelloWorld/HelloWorld.py) integration implementation code for more details.

If the API you are integrating with also supports a query interface using free-form text (i.e. a specific query language implemented in the product), you can also add another parameter (usually called query) that gives users more freedom to generate alerts in Cortex XSIAM based on a specific query. This gives more flexibility to the users and supports more advanced use cases for your integration. The convention is that the query parameter overrides other parameters such as severity and type, as we assume that only advanced users use the query option.

There are additional required parameters for integrations that fetch incidents. You don't need to handle them in your code, but they must be correctly defined in your integration YAML file. You can view the [updated list](https://github.com/demisto/demisto-sdk/blob/f407ffe9d632c45acce0ce0587efbf8ae89d6db8/demisto_sdk/commands/common/constants.py#L870).

</details>

<details>

<summary>Other parameters</summary>

Your product is unique, and so are the parameters you might need to add to the integration. Besides connectivity and fetch parameters, you can add more parameters as you see fit. In general, add parameters whenever you want the users to specify settings that are common across several integration commands.

An example is a Threat Intel reputation threshold. In this scenario, you are creating an integration that asks for reputation about network assets (IP addresses, URLs and domains), using different commands (`!ip`, `!url` and `!domain`). Your API returns a score value between 0 and 100 to determine whether the asset is malicious. The higher the score, the higher the chance the asset is bad. Cortex XSIAM reports whether an indicator is good or bad using the concept of [DBotScore](reputation-and-dbot-score) with a discrete set of values: 0 means unknown, 1 good, 2 suspicious and 3 bad. To map the score that your API returns (0-100) to a DBotScore, you typically define a threshold above which the asset is considered malicious. The value of the threshold is usually a number that you provide as a default (60, for example) but the end user should be able to override the default. Threshold value should be common across all of the different reputation commands (`!ip`, `!url` and `!domain`) of your integration. For this reason, adding threshold as an additional integration parameter is a good practice. Users can set the threshold once and don't have to specify it manually every time to invoke a reputation command. You can still add an optional argument to each command to override the integration parameter if needed.

</details>
