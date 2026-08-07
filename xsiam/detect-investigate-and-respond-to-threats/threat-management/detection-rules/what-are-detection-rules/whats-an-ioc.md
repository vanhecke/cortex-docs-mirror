# What's an IOC?

Indicators of compromise (IOCs) enable Cortex XSIAM to generate issues about known malicious objects on endpoints across the organization. You can load collections of IOCs from threat-intelligence sources into Cortex XSIAM or define them individually.

{% hint style="info" %}
### Note

Cortex XSIAM supports a maximum of 4,000,000 IOCs.
{% endhint %}

You can define the following types of IOCs:

* Full path
* File name
* Domain
* Destination IP address
* MD5 hash
* SHA256 hash

After you load or define IOCs, the tenant checks for matches in the xdr\_data dataset that contains all the information collected about the endpoints and the network. Cortex XSIAM looks for IOC matches in all data collected in the past and continues to evaluate any new data it receives in the future.

Issues for IOCs are identified by the source type of the IOC.
