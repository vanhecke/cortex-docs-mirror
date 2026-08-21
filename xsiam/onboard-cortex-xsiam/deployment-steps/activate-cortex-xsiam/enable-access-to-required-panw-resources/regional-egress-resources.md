---
description: >-
  Configure Cortex XSIAM firewall egress access with regional FQDNs, IP
  addresses, ports, and App-IDs.
---

# Cortex XSIAM regional egress resources

Use these Cortex XSIAM regional egress resources to configure firewall allowlists for your deployment region. They support agent-to-tenant communication for API access, heartbeats, Live Terminal, and EDR data uploads.

The following table describes the service definition, FQDNs, and App-ID coverage for your deployment. Unless specified, all ports are 443 (TCP). Select your region and allow outbound traffic to the corresponding FQDNs and IPs.

### Cortex XSIAM egress service definitions

<table><thead><tr><th>Service Definition</th><th width="295">FQDN</th><th>APP-ID</th></tr></thead><tbody><tr><td><p>Egress tenant</p><p>Connects to the Cortex XSIAM tenant.</p></td><td><code>&#x3C;tenant-name>.xdr.&#x3C;region>.paloaltonetworks.com</code></td><td><code>cortex-xdr</code></td></tr><tr><td><p>Live Terminal</p><p>Used in live terminal flow for real-time shell sessions</p></td><td><p><code>https://lrc-&#x3C;region>.paloaltonetworks.com</code></p><p><code>wss://lrc-&#x3C;region>.paloaltonetworks.com</code></p></td><td><code>cortex-xdr</code></td></tr><tr><td><p>Endpoint Detection and Response (EDR)</p><p>Used for EDR data upload. Includes telemetry logs, process executions, and security events that the Cortex XDR agent captures and sends to the cloud for analysis</p></td><td><code>dc-&#x3C;tenant-name>.traps.paloaltonetworks.com</code></td><td><code>traps-management-service</code></td></tr><tr><td><p>Heartbeat</p><p>Used for all other requests between the XDR agent and the tenant, including heartbeat, uploads, action results, and scan reports.</p></td><td><code>ch-&#x3C;tenant-name>.traps.paloaltonetworks.com</code></td><td><code>traps-management-service</code></td></tr><tr><td><p>API Access</p><p>Used for API requests and responses and to connect to an engine.</p></td><td><code>api-&#x3C;tenant-name>.xdr.&#x3C;region>.paloaltonetworks.com</code></td><td>N/a</td></tr><tr><td><p>Indicator</p><p>Used to download the IOC indicators from the tenant. Downloading lists of bad IPs, domains, or hashes to block locally.</p></td><td><code>xdr-&#x3C;region>-&#x3C;project ID>-tim-indicators.storage.googleapis.com</code></td><td><code>traps-management-service</code></td></tr><tr><td><p>Verdict requests</p><p>Used for get-verdict requests. For example, checking if a specific file hash is known to be malware.</p></td><td><code>cc-&#x3C;tenant-name>.traps.paloaltonetworks.com</code></td><td><code>traps-management-service</code></td></tr><tr><td><p>Broker VM</p><p>Connection for the Broker VM</p></td><td><code>br-&#x3C;tenant-name></code><em><code>.xdr.</code></em><code>&#x3C;region>.paloaltonetworks.com</code></td><td>N/a</td></tr></tbody></table>

The following tables list the required resources by region. Unless specified, all ports are 443 (TCP).

### Cortex XSIAM egress IP addresses in the Americas

<table><thead><tr><th>Region</th><th>Egress (tenant)</th><th width="146">Live Terminal</th><th>EDR &#x26; Heartbeat</th><th>API Access</th><th>Indicator &#x26; Verdict requests</th><th>Broker VM</th></tr></thead><tbody><tr><td>United States (US)</td><td>35.244.250.18</td><td>35.190.88.43</td><td>34.98.77.231</td><td>35.222.81.194</td><td>35.224.140.142</td><td>104.155.131.72</td></tr><tr><td>Brazil (BR)</td><td>34.96.83.202</td><td>34.151.236.197</td><td>136.110.146.246</td><td>34.39.136.78</td><td>34.39.195.104</td><td>35.198.38.182</td></tr><tr><td>Canada (CA)</td><td>34.120.31.199</td><td>35.203.99.74</td><td>34.96.120.25</td><td>35.203.82.121</td><td>35.203.35.23</td><td>34.95.8.232</td></tr></tbody></table>

### Cortex XSIAM egress IP addresses in EMEA

| Region                                | Egress (tenant) | Live Terminal  | EDR & Heartbeat | API Access     | Indicator & Verdict request | Broker VM      |
| ------------------------------------- | --------------- | -------------- | --------------- | -------------- | --------------------------- | -------------- |
| France (FA)                           | 34.111.134.57   | 34.163.57.57   | 34.36.155.211   | 34.155.222.152 | 34.155.110.169              | 34.155.90.61   |
| Germany (DE)                          | 34.98.68.183    | 34.107.61.141  | 34.107.161.143  | 34.107.57.23   | 35.242.201.199              | 35.198.112.13  |
| Israel (IL)                           | 34.111.129.144  | 34.165.43.106  | 34.128.157.130  | 34.165.156.139 | 34.165.2.110                | 34.165.24.222  |
| Italy (IT)                            | 34.8.224.70     | 34.154.154.5   | 34.8.234.58     | 34.154.195.120 | 34.154.230.76               | 34.154.168.139 |
| <p>Netherlands/</p><p>Europe (EU)</p> | 35.227.237.180  | 35.244.251.25  | 34.102.140.103  | 34.90.67.58    | 34.90.71.103                | 34.91.128.226  |
| Poland (PL)                           | 34.117.240.208  | 34.118.62.80   | 35.190.13.237   | 34.116.216.55  | 34.116.213.71               | 34.116.176.97  |
| Qatar (QT)                            | 35.190.0.180    | 34.18.34.73    | 34.107.129.254  | 34.18.46.240   | 34.18.53.229                | 34.18.37.73    |
| Saudi Arabia (SA)                     | 35.244.157.127  | 34.166.54.6    | 34.107.213.85   | 34.166.58.79   | 34.166.53.160               | 34.166.55.153  |
| South Africa (ZA)                     | 34.149.165.12   | 34.35.56.170   | 35.190.79.68    | 34.35.64.191   | 34.35.13.198                | 34.35.45.251   |
| Spain (ES)                            | 34.111.188.248  | 34.175.18.78   | 34.120.102.147  | 34.175.30.176  | 34.175.205.166              | 34.175.182.55  |
| Switzerland (CH)                      | 34.111.6.153    | 34.65.213.226  | 34.149.180.250  | 34.65.248.119  | 34.65.137.215               | 34.65.51.103   |
| United Kingdom (UK)                   | 34.120.87.77    | 35.242.159.176 | 35.244.133.254  | 34.89.56.78    | 34.89.42.214                | 35.197.219.110 |
| Finland (FI)                          | 34.160.63.63    | 34.88.31.230   | 136.110.165.34  | 35.228.73.215  | 35.228.118.177              |                |

### Cortex XSIAM egress IP addresses in JPAC

<table><thead><tr><th>Region</th><th>Egress (tenant)</th><th>Live Terminal</th><th width="143">EDR &#x26; Heartbeat</th><th>API Access</th><th>Indicator &#x26; Verdict Requests</th><th>Broker VM</th></tr></thead><tbody><tr><td>Australia (AU)</td><td>34.120.229.65</td><td>35.244.66.177</td><td>34.102.237.151</td><td>35.189.18.208</td><td>35.201.23.188</td><td>35.244.93.0</td></tr><tr><td>Delhi (DL)</td><td>34.8.67.192</td><td>34.131.116.135</td><td>136.110.132.208</td><td>34.131.165.103</td><td>34.131.47.126</td><td>34.131.131.141</td></tr><tr><td>India (IN)</td><td>35.186.207.80</td><td>35.200.146.253</td><td>34.120.213.187</td><td>35.200.158.164</td><td>35.244.57.196</td><td>35.200.234.99</td></tr><tr><td>Indonesia (ID)</td><td>34.111.58.152</td><td>34.101.214.157</td><td>34.128.156.84</td><td>34.128.115.238</td><td>34.101.155.198</td><td>34.101.101.170</td></tr><tr><td>Japan (JP)</td><td>35.241.28.254</td><td>34.84.201.32</td><td>34.95.66.187</td><td>34.84.125.129</td><td>34.84.225.105</td><td>34.85.74.43</td></tr><tr><td>Singapore (SG)</td><td>34.117.211.129</td><td>34.87.61.186</td><td>34.120.142.18</td><td>34.87.83.144</td><td>35.247.161.94</td><td>34.87.167.125</td></tr><tr><td>South Korea (KR)</td><td>34.54.5.247</td><td>34.22.66.91</td><td>34.54.155.245</td><td>34.64.54.175</td><td>34.64.228.117</td><td>34.64.46.249</td></tr><tr><td>Taiwan (TW)</td><td>34.160.28.41</td><td>34.80.34.30</td><td>34.149.248.76</td><td>35.234.8.249</td><td>35.229.186.216</td><td>34.80.230.166</td></tr></tbody></table>
