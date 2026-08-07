# Import Broker VM Configuration

Learn more about importing one Broker VM configuration to another.

{% hint style="warning" %}
#### Important

This option can only be used on Broker VMs with version 20.0 and later, and is only suitable for importing a configuration of brokers in the same version, or from a broker in an older version to a broker in a newer version.
{% endhint %}

Importing Broker VM configurations allows you to copy, including applet settings, the configuration of one Broker VM to another. The import overrides the Broker VM and applet settings in the target Broker VM.

1. To replace the Broker VM configuration, right-click the Broker VM and select Import Configuration.
2. Select the Broker VM that has the configuration that you want to import.
3. (Optional) After the import is complete and the new configurations are applied to the target Broker VM, you can choose to shutdown the source Broker VM (default configuration). This step ensures that there are no conflicts in data collection and applets operation.

{% hint style="info" %}
#### Note

If this option is selected, the shutdown process can take up to 10 minutes to allow the broker to finish offloading the data cache.
{% endhint %}

4. Select the confirmation checkbox.
5. Click Import. After a successful import, the new configurations are immediately applied to the target Broker VM.

{% hint style="warning" %}
#### Important

If your source Broker VM configuration includes a WEC applet, you'll need to ensure that you update the DNS record of this Broker VM's FQDN to point to the target Broker VM IP address.
{% endhint %}
