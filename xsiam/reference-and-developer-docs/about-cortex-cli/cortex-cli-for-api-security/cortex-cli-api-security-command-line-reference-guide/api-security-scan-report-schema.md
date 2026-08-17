---
description: Reference schema for API Security scan reports.
---

# API Security scan report schema

This schema defines the fields returned by an API Security scan report.

```json
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
