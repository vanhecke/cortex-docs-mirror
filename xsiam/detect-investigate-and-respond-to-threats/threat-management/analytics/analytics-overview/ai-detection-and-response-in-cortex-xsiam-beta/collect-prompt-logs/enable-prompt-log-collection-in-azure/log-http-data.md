# Log HTTP data

Configure logging request and response payloads in Azure API Management.

1. In your Azure API Management instance, navigate to **APIs** → **Select an API**.
2. In the **Settings** tab, under **Diagnostics Settings**, select **Azure Monitor** and select **Enable**.
3. In **Advanced Options** select the following: **Backend Request** and **Backend Response**.
4. For **Backend Request**, enter the following headers:
   * Authorization
   * Api-key
   * User-Agent
   * Referer
   * Host
5. In **Number of payload bytes to log**, enter: **`8192`**. Click **Save**.
6. For **Backend Response**, enter the following headers:
   * apim-request-id
   * x-ms-rai-invoked
7. In **Number of payload bytes to log**, enter: **`8192`**. Click **Save**.

![log-http-data.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-f3d37094d4ced0b74e2aec60dd8a3777310d9124%2F853d6cabdb56e1d5591e221c5082042bcd64d08b3aaa2789019b16e3c4d5e17b.png?alt=media)
