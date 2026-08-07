# Cortex CLI for API Security

API Security testing is implemented in Cortex XSIAM through the Cortex CLI.

This testing evaluates APIs for vulnerabilities and misconfigurations using fuzzing techniques to ensure secure data transmission, prevent unauthorized access, and to ensure that the API behaves as expected under unexpected or malformed input.

{% hint style="warning" %}
### Prerequisite

* Ensure you have the required user permissions. Refer to [Cortex CLI]() for more information
* Onboard and install the Cortex CLI. Refer to [Connect Cortex CLI](connect-cortex-cli) for more information
* Ensure your application exposes APIs and provides a corresponding OpenAPI Specification file
* Ensure that you have installed `Java v 11` and above
{% endhint %}

## Authentication

The authentication file schema defines the authentication method (such as JWT, Basic) used to authorize connections to your scanned application. The following example provides configurations examples for common methods, including Basic authentication, API Keys and bearer tokens.

EXAMPLE

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
        ./cortexcli  --log-level <ERROR LEVEL> –-api-base-url <API URL> --api-key <API key from the "Authenticate" step in the CLI connector screen> --auth-id 1 api scan  --api-spec-file <OPENAPI SPEC LOCATION>   --scanned-app-url <BASE URL OF THE SCANNED APP> --java-location <JAVA BIN LOCATION>
        
```

## Output

The API Security scan generates a detailed scan report that includes:

* **Findings**: These include vulnerabilities and risks identified in the scanned application's APIs, such as SQL Injection, sensitive data leaks, and other issues
* **Errors**: This section lists error responses returned by the scanned application
* **Metadata**: Information such as runtime details, scan status (success or failure), scan duration, hostname and scan parameters

### API Security scan report schema

<details>

<summary>Read more...</summary>

```programlisting
{
  "reportID": "string",
  "results": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "url": "string",
      "method": "string",
      "risk": "string",
      "alert": "string",
      "tags": {},
      "statusCode": "integer",
      "requestBody": "string",
      "curlCommand": "string"
    }
  ],
  "serverErrors": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "url": "string",
      "method": "string",
      "risk": "string",
      "alert": "string",
      "tags": {},
      "statusCode": "integer",
      "requestBody": "string",
      "curlCommand": "string"
    }
  ],
  "scanStartTime": "string (ISO 8601 datetime)",
  "elapsedSeconds": "number",
  "hostname": "string",
  "scanStatus": "string",
  "parameters": {
    "scannedAppURL": "string",
    "apiSpecFile": "string",
    "apiSpecType": "string",
    "timeoutSeconds": "integer"
  }
}
          
      
```

</details>

### API Security scan output example

<details>

<summary>Read more...</summary>

```programlisting
{
  "reportID": "0a739ae6-d18e-11ef-8a06-263731778ec0",
  "results": [
    {
      "id": "0",
      "name": "Server Leaks Version Information via \"Server\" HTTP Response Header Field",
      "description": "The web/application server is leaking version information via the \"Server\" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to.",
      "url": "http://localhost:5000/api/v1/extract",
      "method": "POST",
      "risk": "Low",
      "alert": "Server Leaks Version Information via \"Server\" HTTP Response Header Field",
      "tags": {
        "CWE-200": "https://cwe.mitre.org/data/definitions/200.html",
        "OWASP_2017_A06": "https://owasp.org/www-project-top-ten/2017/A6_2017-Security_Misconfiguration.html",
        "OWASP_2021_A05": "https://owasp.org/Top10/A05_2021-Security_Misconfiguration/",
        "WSTG-v42-INFO-02": "https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/01-Information_Gathering/02-Fingerprint_Web_Server"
      },
      "statusCode": 404,
      "requestBody": "--d3b92f4f-e2e3-4caa-8b00-4e43c8df0d87\r\nContent-Disposition: form-data; name=\"file\"\r\nContent-Type: text/plain\r\n\r\n\"John Doe\"\r\n--d3b92f4f-e2e3-4caa-8b00-4e43c8df0d87--",
      "curlCommand": "curl -X POST \"http://localhost:5000/api/v1/extract\" -H host: localhost:5000 -H user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0 -H pragma: no-cache -H cache-control: no-cache -H accept: application/json -H content-type: multipart/form-data; boundary=d3b92f4f-e2e3-4caa-8b00-4e43c8df0d87 -H content-length: 165 -d '--d3b92f4f-e2e3-4caa-8b00-4e43c8df0d87\r\nContent-Disposition: form-data; name=\"file\"\r\nContent-Type: text/plain\r\n\r\n\"John Doe\"\r\n--d3b92f4f-e2e3-4caa-8b00-4e43c8df0d87--'"
    }
  ],
  "serverErrors": [],
  "scanStartTime": "2025-01-13T11:09:04.919359+02:00",
  "elapsedSeconds": 1.349090375,
  "hostname": "My Computer",
  "scanStatus": "Failed",
  "parameters": {
    "scannedAppURL": "http://localhost:5000",
    "apiSpecFile": "openapi.json",
    "apiSpecType": "openapi",
    "timeoutSeconds": 300
  }
}
        
```

</details>
