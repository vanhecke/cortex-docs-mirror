---
description: >-
  Commands generalized across similar integrations to enable combining data from
  various sources or running integrations in parallel.
---

# Generic commands

The Cortex XSIAM platform supports hundreds of integrations. Among similar integrations, some commands can be generalized to enable combining data from various sources or running integrations in parallel.

For example, reputation commands such as `!file` can gather reputation from multiple connected integrations to one indicator.

These commands can be used on all integrations or with the `using` parameter on specific integration instances.

**Generic reputation commands**

Cortex XSIAM supports many integrations with reputation providers, for example, VirusTotal, AlienVault OTX, and MISP. Every integration that returns a reputation about an indicator must implement the generic reputation commands and calculate a [DBot Score](reputation-and-dbot-score).

When creating commands that enrich indicators, the commands should be named according to the indicator, such as `!ip` and `!domain`. This naming convention allows commands from multiple integrations to be run together to enrich an indicator. For example, running `!ip ip=8.8.8.8` can trigger multiple integrations that gather information about the IP address.

The recommended way to return indicator context is using one of the classes under `Common` (`Common.IP`, `Common.URL`). For more information, see Return IP Reputation in [Context and outputs](context-and-outputs). An example of returning indicators is the [IPinfo v2](https://cortex.marketplace.pan.dev/marketplace/details/ipinfo/) integration.

The following are available generic reputation commands.

<details>

<summary>file</summary>

Runs reputation on files.

```programlisting
- name: file
   arguments:
   - name: file
     default: true
     description: List of files.
     isArray: true
```

</details>

<details>

<summary>ip</summary>

Runs reputation on IPs.

```programlisting
- name: ip
   arguments:
   - name: ip
     default: true
     description: List of IPs.
     isArray: true
```

</details>

<details>

<summary>url</summary>

Runs reputation on URLs.

```programlisting
- name: url
   arguments:
   - name: url
     default: true
     description: List of URLs.
     isArray: true
```

</details>

<details>

<summary>domain</summary>

Runs reputation on domains.

```programlisting
- name: domain
   arguments:
   - name: domain
     default: true
     description: List of domains.
     isArray: true
```

</details>

<details>

<summary>email</summary>

Runs reputation on emails.

```programlisting
- name: email
   arguments:
   - name: email
     default: true
     description: List of emails.
     isArray: true
```

</details>

<details>

<summary>cve</summary>

Runs reputation on CVEs.

```programlisting
- name: cve
   arguments:
   - name: cve
     default: true
     description: List of CVEs.
     isArray: true
```

</details>

**Generic endpoint command**

Cortex XSIAM supports many integrations with endpoint providers, for example, GuardiCoreV2.

The following is the generic endpoint command.

**endpoint**

Returns information about an endpoint.

```programlisting
- name: endpoint
   arguments:
   - default: false
     description: The endpoint ID.
     isArray: false
     name: id
     required: false
     secret: false
    - default: true
     description: The endpoint IP address.
     isArray: false
     name: ip
     required: false
     secret: false
    - default: false
     description: The endpoint hostname.
     isArray: false
     name: hostname
     required: false
     secret: false
    deprecated: false
```
