# Configure the engine to use a web proxy

Proxy settings can be configured in an engine by adding them as an engine configuration.

{% hint style="info" %}
You need to [configure Docker](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy) to use a proxy. When using a BlueCoat proxy, ensure you encode the values correctly.
{% endhint %}

1.  On the machine on which you installed the engine, navigate to the `d1.conf` file and add the following keys.

    | Key           | Value                                                                                                                                      | Description                                                                                 |
    | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
    | `http_proxy`  | <p><code>http://``&#x3C;user:password@proxy-server:port#></code></p><p>For example <code>http://user:password@proxy-server:3128</code></p> | Environment uses HTTP proxy. Special characters must be escaped.                            |
    | `https_proxy` | <p><code>https://``user:password@proxy-server:port#</code></p><p>For example, <code>https://user:password@proxy-server:3128</code></p>     | Environment uses HTTPS proxy. Special characters must be escaped.                           |
    | `no_proxy`    | <p><code>http://``&#x3C;user:password@proxy-server:port#></code></p><p>For example <code>http://user:password@proxy-server:3128</code></p> | For specific addresses, a proxy bypass will be applied. Special characters must be escaped. |
2.  If the environment variables are not set, or you wish to use different settings than those specified in the environment variables, set the configuration with your specific proxy details in the **`d1.conf`** file. For example:

    ```programlisting
    {"http_proxy": "http://proxy.host.local:8080",
    "https_proxy": "https://proxy.host.local:8443"
    "no_proxy": "https://proxy.host.local:8020"}
    ```
3. Save the file.
4.  On the machine where you installed the engine, navigate to the `upgrade.conf` file and edit the file to set `https_proxy` to your proxy address. For example, `https_proxy="https://proxy.host.local:8443"`.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>In an environment with a single engine, go to <code>/usr/local/demisto/upgrade.conf</code>. In an environment with multiple engines, go to <code>/usr/local/demisto/&#x3C;engine-name>/upgrade.conf</code>, replacing &#x3C;engine-name> with the name of the engine.</p><p>Note that the key is in the <code>upgrade.conf</code> file and must be <code>https_proxy</code>, even if your proxy address starts with <code>http://</code>.</p></div>
5. Save the file.
