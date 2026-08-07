# Detectors connected to URL and File log types

If you turn off **URL and File log types collection**, some detectors are unable to detect cyber attacks or provide full context, and correlation rules are unable to detect cyber events.

The following detectors are affected by URL logs:

<details>

<summary>Read more...</summary>

* A non-browser process accessed a website UI
* Reverse SSH tunnel to external domain/IP
* Uncommon network tunnel creation
* Suspicious domain fronting behavior
* Possible watering hole SMB credential theft
* Rare connection to external IP address or host by an application using RMI-IIOP or LDAP protocol
* Uncommon JA3 SSL fingerprint communication to an instant messaging server
* PowerShell Initiates a Network Connection to GitHub
* Non-browser failed access to a pastebin-like site
* Non-browser access to a pastebin-like site
* C2 from contextual causality signal
* Massive upload to a rare storage or mail domain
* DNS Tunneling

</details>

The following detectors are affected by File logs:

<details>

<summary>Read more...</summary>

* Rare AppID usage to a rare destination
* Abnormal network communication through TOR using an uncommon port
* Recurring access to rare IP
* Possible network connection to a TOR relay server
* A user accessed an uncommon AppID
* Large Upload (Generic)
* Large Upload (FTP)
* Large Upload (SMTP)
* Possible network connection to a TOR relay server
* A user accessed a resource for the first time via SSO - silent
* Access to a domain that is categorized as malicious - silent
* Recurring access to a rare domain categorized as malicious - silent
* Cloud Large Upload (Generic) - disabled

</details>
