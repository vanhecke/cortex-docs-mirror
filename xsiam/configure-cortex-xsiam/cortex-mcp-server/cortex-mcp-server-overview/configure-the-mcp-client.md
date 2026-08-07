# Configure the MCP client

After you have downloaded and installed the Cortex MCP server, you need to configure your local MCP client to communicate with the Cortex MCP server. The instructions below use Claude Desktop, but any MCP client can be used.

1.  In the Claude Desktop app, navigate to **Settings** → **Developer** → **Edit Config**. The configuration file opens in your default text editor.

    For reference, the file is located at:

    * macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
    * Windows: `%APPDATA%\Claude\claude_desktop_config.json`
2.  Add the `mcpServers` configuration to the file. The examples below are provided for container (Docker) and local client (Poetry virtual environment). The exact details of your `mcpServers` configuration depend on your specific installation.

    **Docker Container**

    ```programlisting
    {
      "mcpServers": {
        "Cortex MCP Server": {
          "command": "docker",
          "args": [
            "run",
            "--env-file",
            "/path/to/.env",
            "-i",
            "--rm",
            "cortex-mcp"
          ]
        }
      }
    }
    ```

    **Poetry virtual environment**

    ```programlisting
    {
      "mcpServers": {
        "Cortex MCP Server": {
          "command": "python",
          "args": [
            "/path/to/cortex-mcp/src/main.py"
          ],
           "env": {
              "CORTEX_MCP_PAPI_URL": "https://api.cortex.example.com",
              "CORTEX_MCP_PAPI_AUTH_HEADER": "<your_api_key>", 
              "CORTEX_MCP_PAPI_AUTH_ID": "<your_api_key_id",
              "MCP_TRANSPORT": "stdio/streamable-http"
       }
        }
      }
    }
    ```
3. Save the changes to the configuration file and restart Claude Desktop for the changes to take effect.
4. Verify the connection to the Cortex MCP server. You should see the Cortex MCP server running in the Developer settings and a hammer icon may appear in the input box, indicating the MCP tools are available.
