# Create custom Cortex MCP server tools

You can build your own tools using OpenAPI or Python to manage cases, handle issues, and conduct investigations. More detailed information can be found in the README file located in the `src/usecase` directory. Tools are based on Cortex API endpoints.

To view the Cortex XSIAM API documentation, see [Cortex XSIAM APIs](https://app.gitbook.com/s/1ZrobAtcwfCDWAJAWeuj/).

Any new or updated components provided by Cortex are automatically downloaded into the builtin\_components folder. During each update, the folder is fully replaced and all existing contents are recreated. Do not add custom tools to this directory, as it is managed entirely by Cortex and is overwritten at every update.

### **OpenAPI**

You can create an OpenAPI specification for a specific API endpoint.

1. Create a YAML file in the `/custom_components/openapi` directory with the name of the MCP component. For example: `custom_cortex_component.yaml`.
2. Base your custom OpenAPI component on the Cortex API documentation structure for a specific endpoint. We recommend viewing the built-in tools, located at `/builtin_components/openapi`, as a reference.
3. After you define the OpenAPI specification, the Cortex MCP server collects it automatically, and it is ready for use.
4. Test your new MCP component by running the Cortex MCP server and writing a prompt that uses your new component.

### **Python**

We recommend using Python for more complex MCP components that require custom logic. MCP components in Python are defined in a module.

1. Create a new Python file in the `/custom_components` directory.
2. Define a class that inherits from the `BaseModule` class with the required methods. We recommend viewing the built-in modules, located at `/builtin_components`, as a reference.
3. After you define a class, the Cortex MCP server collects it automatically and it is ready for use.
4. Test your new MCP component by adding an end-to-end test in the `tests/e2e` directory, or run the MCP server and write a prompt that uses your new component.
