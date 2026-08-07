# Data sources and supported services

AIDR uses multiple data sources to gain visibility into AI usage in the cloud and identify AI-specific threats. Cloud audit logs are used for infra-level detections, such as model theft, denial of ML service, and training data poisoning. Cloud audit logs can be collected using existing data collectors. At this time, prompt logs are used to detect which models are being used.

See [Collect prompt logs](collect-prompt-logs) for instructions on configuring prompt log collection.

The following AI/ML managed services are supported:

* AWS: Amazon Bedrock, SageMaker
* Azure: Open AI
* GCP: VertexAI
