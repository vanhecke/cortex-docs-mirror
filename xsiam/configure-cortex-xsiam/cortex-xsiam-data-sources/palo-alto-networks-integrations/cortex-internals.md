# Cortex Internals

{% hint style="warning" %}
**Important**

This connector is only available for tenants that onboarded after July 26, 2026. For tenants that onboarded before this date, use Marketplace to access the standalone integration. For more information, see [Marketplace](../../marketplace).
{% endhint %}

This sub-capability is available with any active Cortex XSIAM, Cortex Cloud Posture Security, Cortex Cloud, Cortex Cloud Runtime Security, Cortex XDR, or Cortex AgentiX license.

The Cortex Internals connector provides native locking integrations (Core Lock and Demisto Lock) that prevent concurrent execution of scripts or commands, using a wait-lock-release flow (mutex). Use the lock name argument to support multiple locks in different flows. These are native integrations that do not require configuration.

This connector includes the following sub-capabilities (Marketplace integrations link to PAN DEV for more information):

* [Core Lock](https://xsoar.pan.dev/docs/reference/integrations/core-lock): Locking mechanism that prevents concurrent execution of different tasks.
* [Demisto Lock](https://xsoar.pan.dev/docs/reference/integrations/demisto-lock): Locking mechanism that prevents concurrent execution of different tasks.

To configure this connector, follow the steps outlined in the configuration wizard.
