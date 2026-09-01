---
description: Use Elasticsearch Filebeat data with Cortex XSIAM.
---

# Elasticsearch Filebeat

{% hint style="info" %}
**Note**

You can configure collecting container logs from Google Kubernetes Engine using Elasticsearch Filebeat with a Custom - Filebeat based Collector or with a content pack Integration. For more information, see [Google Kubernetes Engine](../google/google-kubernetes-engine).
{% endhint %}

You can ingest logs related to file activity on your endpoints and servers without using the Cortex XDR agent by installing Elasticsearch Filebeat as a system logger and then forward those logs to Cortex XSIAM using a Custom - Filebeat based Collector.

| Collection Method                                                             | Description                                                                                                       |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Custom - Filebeat based Collector (standard data source) overview             | Forward logs from Elasticsearch Filebeat to Cortex XSIAM using the Custom - Filebeat based Collector data source. |
| Link to custom - Filebeat based Collector (standard data source) instructions | [Ingest logs from Elasticsearch Filebeat](elasticsearch-filebeat/ingest-logs-from-elasticsearch-filebeat)         |
