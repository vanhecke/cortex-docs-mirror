# Forward notifications to webhook

You can forward issues and cases to webhook.

{% hint style="info" %}
### Note

Cortex sends webhook notifications using its own predefined payload format. If your webhook endpoint requires the payload to be structured in a specific way — for example, the format expected by Google Chat or another third-party service — the notification will not be delivered successfully. Only endpoints that accept arbitrary JSON payloads are supported.
{% endhint %}

Configure access in your firewall

Add the IP addresses for your tenant region to your firewall. For more information, refer to the list of ingress IPs in [Enable access to required PANW resources](../../../../deployment-steps/activate-cortex-xsiam/enable-access-to-required-panw-resources).

Configure egress in Cortex Gateway

Before forwarding cases or issues to Splunk, you need to configure egress. Only a user with Account Admin or Instance Admin permissions can configure egress.

To configure egress, you need to enter the FQDN (fully qualified domain name), without including the port or the path. For example, if the full URL is `https://webhook..mycompany.com/target_resource`, you would enter `webhook.mycompany.com`.

1. In the Cortex Gateway, go to **Permission Management** → **Egress Configurations** → **Path**.
2. Select the account name and tenant.
3. In the Flow field, select **Webhook**.
4. Enter the FQDN (full qualified domain name) of the webhook endpoint. For example, `webhook.mycompany.com`. Note that the path does not include HTTP or HTTPS.
5. Add the configuration.

Complete external application configuration in Cortex XSIAM

1. Go to **Settings** → **Configurations** → **Integrations** → **External Applications** → **Add Application** and select **Webhook**.
2. Enter the webhook URL. The URL can include a port, but the connection must be HTTPS.
3. Click **Verify**. If egress has not been configured in the Cortex Gateway, verification will fail.
4. After verification is successful, enter the instance name and optional description.
5. Show advanced settings to add HTTPS headers if required.
6. Enter the authentication token for secure access to your Splunk instance.
7. Click **Test** to verify the connection, then click **Connect**.

Configure notification forwarding

Follow the instructions for [Configure notification forwarding](../configure-notification-forwarding).
