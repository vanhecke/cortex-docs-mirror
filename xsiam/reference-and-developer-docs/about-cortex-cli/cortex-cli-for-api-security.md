---
description: Use Cortex CLI for API Security scans in Cortex XSIAM.
---

# Cortex CLI for API Security

API Security testing is implemented in Cortex Cloud through the Cortex CLI.

This testing evaluates APIs for vulnerabilities and misconfigurations using fuzzing techniques to ensure secure data transmission, prevent unauthorized access, and to ensure that the API behaves as expected under unexpected or malformed input.

{% hint style="warning" %}
### Prerequisite

* Ensure you have the required user permissions. Refer to [About Cortex CLI]() for more information
* Onboard and install the Cortex CLI. Refer to [Connect Cortex CLI](connect-cortex-cli) for more information
* Ensure your application exposes APIs and provides a corresponding OpenAPI Specification file
* Ensure that you have installed `Java v 11` and above
{% endhint %}

## Authentication

The authentication file schema defines the authentication method (such as JWT, Basic) used to authorize connections to your scanned application. The following example provides configurations examples for common methods, including Basic authentication, API Keys and bearer tokens.

EXAMPLE: Authentication File Schema Example

```programlisting
type: headers
creds:
    name: <header name>
    value: <header value>
------------------------------------
For basic auth
type: basic
creds:
    username: {USERNAME}
    password: {PASSWORD}
------------------------------------
For API Keys
type: headers
creds:
    name: x-api-key
    value: {API key}
------------------------------------
For Bearer tokens
type: headers
creds:
    name: Authorization
    value: Bearer {BEARER_TOKEN} 
```

## Run API Security scans

To scan API Security, run:

```programlisting
        ./cortexcli  --log-level <ERROR LEVEL> –-api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --api-key-id 1 api scan  --api-spec-file <OPENAPI SPEC LOCATION>   --scanned-app-url <BASE URL OF THE SCANNED APP> --java-location <JAVA BIN LOCATION>
        
```

## Output

The API Security scan generates a detailed scan report that includes:

* **Findings**: These include vulnerabilities and risks identified in the scanned application's APIs, such as SQL Injection, sensitive data leaks, and other issues
* **Errors**: This section lists error responses returned by the scanned application
* **Metadata**: Information such as runtime details, scan status (success or failure), scan duration, hostname and scan parameters

### API Security scan report schema

Review the [API Security scan report schema](cortex-cli-for-api-security/cortex-cli-api-security-command-line-reference-guide/api-security-scan-report-schema) for report fields and types.

### API Security scan output example

Review the [API Security scan output example](cortex-cli-for-api-security/cortex-cli-api-security-command-line-reference-guide/api-security-scan-output-example) to see a complete report.
