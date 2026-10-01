# Required APIs

### Why Enabling APIs is Required

In Google Cloud Platform (GCP), services operate under a modular, opt-in architecture. By default, a newly created GCP project keeps the vast majority of Google Cloud APIs disabled. Enabling specific APIs during onboarding grants your project explicit permission to interact with the underlying Google Cloud services. If a required API is disabled, Cortex XSIAM cannot access that service, preventing us from discovering or scanning those assets.

The list below covers all APIs Cortex XSIAM needs to run full asset discovery across every supported GCP service. This is not tied to which security capabilities you have configured. If you have not enabled DSPM, for instance, Cortex XSIAM still discovers your database assets, but it does not scan them. The APIs control what we can see, not what we act on.

Your deployment may only use a subset of these services. Enabling the full list ensures complete coverage and allows Cortex XSIAM to maintain a real-time, up-to-date asset inventory across all your services, even as your usage expands.

### Where to enable each API

Enabling an API is a per-project action in GCP. There is no organization-level or folder-level equivalent. Even when you onboard a whole organization, and even when Cortex XSIAM queries that organization through a single organization-scoped API call, each individual project still decides for itself whether a given API is on or off.

This means you cannot satisfy the requirements below by enabling everything in one place. Cortex XSIAM uses two distinct kinds of GCP project, and each one needs a different set of APIs:

| Scope                       | What it refers to                                                                                                                                                                               | What breaks if APIs are missing                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Service account project** | The single GCP project that hosts the Cortex XSIAM service account created during onboarding. This is the project you supply as the hosting project in the onboarding template.                 | Onboarding fails outright, or the connector cannot authenticate, enumerate your hierarchy, or deliver audit logs. |
| **Scanned projects**        | Every GCP project inside the onboarded scope. For an organization, this is every project under the organization, including projects added later. For a folder, every project under that folder. | Onboarding appears to succeed, but assets in the affected projects are silently missing from your inventory.      |

The second failure mode is the one to watch for. A project with a disabled API does not produce an error during onboarding. It simply never appears in your asset inventory, so the gap is easy to miss until you notice the project's resources are absent.

We recommend creating the Cortex XSIAM service account in a dedicated GCP project rather than in a project that runs production workloads. GCP applies API quotas per project, and a dedicated project keeps Cortex XSIAM's API traffic from competing with your own services for quota.

#### **Core APIs**

Enable core APIs on the service account project and on every scanned project. These four APIs are the foundation of GCP asset discovery. Enable each one on the service account project and on every project within the onboarded scope. Missing any of them on a given project means Cortex XSIAM cannot see that project's assets at all.<br>

| API                                                                                                  | Purpose                                                                                                                     | Why every scanned project needs it                                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [cloudasset.googleapis.com](https://docs.cloud.google.com/asset-inventory/docs/reference/rest)       | Cloud Asset Inventory. The primary mechanism Cortex XSIAM uses to export and search GCP resource metadata and IAM policies. | Cortex XSIAM issues a single Cloud asset inventory request scoped to your organization or folder, but Cloud asset inventory only returns metadata for a project when the Cloud Asset API is enabled on that project. Projects with the API disabled are omitted from the response and no error is raised. |
| [cloudresourcemanager.googleapis.com](https://docs.cloud.google.com/resource-manager/reference/rest) | Cloud Resource Manager. Reads the organization, folder, and project hierarchy.                                              | Cortex XSIAM walks your hierarchy to enumerate folders and projects and to attach each discovered asset to its owning project. A project that cannot be read is not scanned.                                                                                                                              |
| [serviceusage.googleapis.com](https://docs.cloud.google.com/service-usage/docs/reference/rest)       | Service Usage. Reports which APIs are enabled on a project.                                                                 | Before scanning a project, Cortex XSIAM asks Service Usage which services are actually in use there, then skips collection for the rest. Without this API, Cortex XSIAM cannot determine what to collect and skips the project. This API also governs the quota that Cortex XSIAM's calls consume.        |
| [iam.googleapis.com](https://docs.cloud.google.com/iam/docs/reference/rest)                          | Identity and Access Management. Reads roles, service accounts, and workload identity configuration.                         | Identity and entitlement findings are computed per project. Projects without this API contribute no identity data.                                                                                                                                                                                        |

{% hint style="info" %}
**Note**: Enabling the Cloud Asset API on every scanned project is required even for organization-level onboarding. This is the most common cause of projects missing from the Cortex XSIAM asset inventory after an otherwise successful organization onboarding.
{% endhint %}

#### Connector APIs

Enable connector APIs on the service account project only. These APIs support the Cortex XSIAM connector infrastructure itself. They are only needed in the project that hosts the service account.

| API                                                                                                        | Purpose                                                                                      | Required for               |
| ---------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------- |
| [logging.googleapis.com](https://docs.cloud.google.com/logging/docs/reference/v2/rest?rep_location=global) | Cloud Logging. Backs the organization-level log sink that forwards audit log activity.       | Audit log collection       |
| [pubsub.googleapis.com](https://docs.cloud.google.com/pubsub/docs/reference/rest?rep_location=global)      | Cloud Pub/Sub. Hosts the topic and subscription that receive audit log events from the sink. | Audit log collection       |
| [storage.googleapis.com](https://docs.cloud.google.com/storage/docs/apis)                                  | Cloud Storage. Receives Cloud Asset Inventory exports before Cortex XSIAM ingests them.      | Asset inventory collection |

{% hint style="info" %}
**Note**: The onboarding Terraform template creates the log sink at the organization level with child inclusion enabled, and routes every project's audit logs to a single Pub/Sub topic in the service account project. You do not need to enable Cloud Logging or Pub/Sub on individual scanned projects for audit log collection.
{% endhint %}

#### Service discovery APIs

Enable service discovery APIs on every scanned project that runs the service. Each API below lets Cortex XSIAM discover the resources of one GCP service. Enable an API on every project where that service is in use. If a project does not run a given service, that project does not need the corresponding API.

Enabling the full list on all projects is the simplest approach and guarantees coverage as your usage grows. Cortex XSIAM checks Service Usage first and skips collection for services that are not in use, so enabling an unused API adds no scanning overhead.

| API                                                                                                                                       | Description                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| [accessapproval.googleapis.com](https://docs.cloud.google.com/assured-workloads/access-approval/docs/reference/rest)                      | Access Approval — Requires explicit organization consent before Google administrators can access stored data.                               |
| [accesscontextmanager.googleapis.com](https://docs.cloud.google.com/access-context-manager/docs/reference/rest)                           | Access Context Manager — Defines fine-grained, attribute-based access control rules for resources.                                          |
| [admin.googleapis.com](https://developers.google.com/workspace/admin/directory/reference/rest)                                            | Workspace Admin API — Automates administrative actions across Google Workspace users, domains, and groups.                                  |
| [aiplatform.googleapis.com](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest)                                | Vertex AI Platform — Trains, deploys, and manages machine learning models and generative AI workflows.                                      |
| [alloydb.googleapis.com](https://docs.cloud.google.com/alloydb/docs/reference/rest?rep_location=global)                                   | AlloyDB for PostgreSQL — Fully managed PostgreSQL-compatible database built for high-end enterprise analytical and transactional workloads. |
| [analyticshub.googleapis.com](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest)                                   | Analytics Hub — Data exchange platform allowing organizations to share BigQuery datasets securely.                                          |
| [apigateway.googleapis.com](https://docs.cloud.google.com/config-connector/docs/reference/resource-docs/apigateway/apigatewayapi)         | API Gateway — Securely manages and routes traffic to backend APIs, Cloud Functions, or Cloud Run endpoints.                                 |
| [apigee.googleapis.com](https://docs.cloud.google.com/apigee/docs/reference/apis/apigee/rest)                                             | Apigee API Management — Designs, secures, analyzes, and scales enterprise API gateways.                                                     |
| [apihub.googleapis.com](https://docs.cloud.google.com/apigee/docs/reference/apis/apihub/rest)                                             | API Hub — Centralized internal inventory and catalog for organizing organizational API assets.                                              |
| [apikeys.googleapis.com](https://docs.cloud.google.com/api-keys/docs/reference/rest)                                                      | API Keys API — Creates, restricts, and manages API authentication key strings.                                                              |
| [appengine.googleapis.com](https://docs.cloud.google.com/appengine/docs/admin-api/reference/rest)                                         | App Engine — Web Platform-as-a-Service (PaaS) for building and hosting web applications at scale.                                           |
| [artifactregistry.googleapis.com](https://docs.cloud.google.com/artifact-registry/docs/reference/rest?rep_location=global)                | Artifact Registry — Stores and manages container images, language packages (Maven, npm, PyPI), and OS packages.                             |
| [backupdr.googleapis.com](https://docs.cloud.google.com/backup-disaster-recovery/docs/reference/rest?rep_location=global)                 | Backup and DR Service — Centralizes backup, recovery, and disaster recovery policies for enterprise workloads.                              |
| [baremetalsolution.googleapis.com](https://docs.cloud.google.com/bare-metal/docs/reference/rest)                                          | Bare Metal Solution — Provisions dedicated hardware directly inside Google data centers for specialized workloads.                          |
| [batch.googleapis.com](https://docs.cloud.google.com/batch/docs/reference/rest)                                                           | Cloud Batch — Schedules, manages, and executes large-scale batch processing, HPC, and AI workloads.                                         |
| [biglake.googleapis.com](https://docs.cloud.google.com/lakehouse/docs/reference/rest)                                                     | BigLake — Storage engine unifying BigQuery and open-source formats across data lakes.                                                       |
| [bigquery.googleapis.com](https://docs.cloud.google.com/bigquery/docs/reference/rest)                                                     | BigQuery — Serverless, highly scalable enterprise data warehouse for running SQL analytics.                                                 |
| [bigquerydatapolicy.googleapis.com](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest)                        | BigQuery Data Policy — Sets security controls for row-level and column-level data masking in BigQuery.                                      |
| [bigquerydatatransfer.googleapis.com](https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest?rep_location=global)        | BigQuery Data Transfer Service — Automates data ingestion into BigQuery from external databases and SaaS tools.                             |
| [bigqueryreservation.googleapis.com](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest)                             | BigQuery Reservation API — Allocates compute capacity (slots) and flat-rate pricing models for BigQuery queries.                            |
| [bigtableadmin.googleapis.com](https://docs.cloud.google.com/bigtable/docs/reference/admin/rest)                                          | Cloud Bigtable Admin — Manages administrative lifecycle tasks for scalable NoSQL wide-column database clusters.                             |
| [binaryauthorization.googleapis.com](https://docs.cloud.google.com/binary-authorization/docs/reference/rest)                              | Binary Authorization — Enforces software supply chain safety by ensuring only trusted container images deploy.                              |
| [certificatemanager.googleapis.com](https://docs.cloud.google.com/certificate-manager/docs/reference/certificate-manager/rest)            | Certificate Manager — Provisions and manages public and private SSL/TLS certificates for Google Cloud load balancers.                       |
| [ces.googleapis.com](https://docs.cloud.google.com/gemini-enterprise-cx/cx-agent-studio/reference/mcp)                                    | Customer Environment Services — Internal APIs supporting Google Cloud Support operations and environment health monitoring.                 |
| [cloudbilling.googleapis.com](https://docs.cloud.google.com/billing/docs/reference/rest)                                                  | Cloud Billing API — Programmatically monitors costs, pulls invoice data, and manages billing account setups.                                |
| [cloudbuild.googleapis.com](https://docs.cloud.google.com/build/docs/api/reference/rest?rep_location=global)                              | Cloud Build — Continuous integration and continuous delivery (CI/CD) serverless platform.                                                   |
| [clouddeploy.googleapis.com](https://docs.cloud.google.com/deploy/docs/api/reference/rest?rep_location=global)                            | Cloud Deploy — Managed continuous delivery service automating releases to Cloud Run and Kubernetes (GKE).                                   |
| [cloudfunctions.googleapis.com](https://docs.cloud.google.com/functions/docs/reference/rest)                                              | Cloud Functions — Event-driven Function-as-a-Service (FaaS) running serverless code snippets.                                               |
| [cloudidentity.googleapis.com](https://docs.cloud.google.com/identity/docs/reference/rest)                                                | Cloud Identity — Manages identities, users, mobile devices, and security groups across Google services.                                     |
| [cloudkms.googleapis.com](https://docs.cloud.google.com/kms/docs/reference/rest?rep_location=global)                                      | Cloud Key Management Service — Manages encryption keys (symmetric/asymmetric) and cryptographic hardware (HSM).                             |
| [cloudscheduler.googleapis.com](https://docs.cloud.google.com/scheduler/docs/reference/rest)                                              | Cloud Scheduler — Fully managed enterprise cron job scheduler for triggering recurring operations.                                          |
| [cloudsupport.googleapis.com](https://docs.cloud.google.com/support/docs/reference/rest)                                                  | Cloud Support API — Creates and manages technical support cases programmatically with Google Cloud Support.                                 |
| [cloudtasks.googleapis.com](https://docs.cloud.google.com/tasks/docs/reference/rest)                                                      | Cloud Tasks — Asynchronous execution service for distributing task queues across microservices.                                             |
| [composer.googleapis.com](https://docs.cloud.google.com/composer/docs/reference/rest)                                                     | Cloud Composer — Managed workflow orchestration built on Apache Airflow.                                                                    |
| [compute.googleapis.com](https://docs.cloud.google.com/compute/docs/reference/rest/v1)                                                    | Compute Engine — Creates and manages Virtual Machine (VM) instances, disks, and network settings.                                           |
| [connectors.googleapis.com](https://docs.cloud.google.com/integration-connectors/docs/reference/rest)                                     | Integration Connectors — Connects Google Cloud integration services to enterprise applications and SaaS platforms.                          |
| [contactcenterinsights.googleapis.com](https://docs.cloud.google.com/gemini-enterprise-cx/insights/reference/rest)                        | Contact Center AI Insights — Applies natural language processing to customer service call logs and transcripts.                             |
| [container.googleapis.com](https://docs.cloud.google.com/kubernetes-engine/docs/reference/rest)                                           | Google Kubernetes Engine (GKE) — Managed Kubernetes service for deploying, scaling, and running container workloads.                        |
| [containeranalysis.googleapis.com](https://docs.cloud.google.com/artifact-analysis/docs/reference/rest?rep_location=global)               | Container Analysis — Scans container image vulnerabilities and stores supply chain security metadata.                                       |
| [dataflow.googleapis.com](https://docs.cloud.google.com/dataflow/docs/reference/rest?rep_location=global)                                 | Dataflow — Stream and batch data processing service running Apache Beam pipelines.                                                          |
| [dataform.googleapis.com](https://docs.cloud.google.com/dataform/reference/rest?rep_location=global)                                      | Dataform — Transforms, tests, and manages SQL data models directly within BigQuery data warehouses.                                         |
| [datafusion.googleapis.com](https://docs.cloud.google.com/data-fusion/docs/reference/rest)                                                | Cloud Data Fusion — Visual, drag-and-drop ETL data integration service built on open-source CDAP.                                           |
| [datamigration.googleapis.com](https://docs.cloud.google.com/database-migration/docs/reference/rest?rep_location=global)                  | Database Migration Service — Automates serverless migrations to Cloud SQL and AlloyDB with minimal downtime.                                |
| [datapipelines.googleapis.com](https://docs.cloud.google.com/dataflow/docs/reference/data-pipelines/rest)                                 | Data Pipelines — Schedules and monitors recurring Dataflow streaming or batch pipelines.                                                    |
| [dataplex.googleapis.com](https://docs.cloud.google.com/dataplex/docs/reference/rest)                                                     | Dataplex — Provides data management, governance, and discovery across distributed data lakes.                                               |
| [dataproc.googleapis.com](https://docs.cloud.google.com/managed-spark/docs/reference/rest)                                                | Dataproc — Runs managed Apache Spark, Hadoop, and Presto clusters for large-scale data processing.                                          |
| [datastore.googleapis.com](https://docs.cloud.google.com/datastore/docs/reference/data/rest?rep_location=global)                          | Cloud Datastore — Legacy NoSQL document database (auto-upgraded to Cloud Firestore in Datastore mode).                                      |
| [datastream.googleapis.com](https://docs.cloud.google.com/datastream/docs/reference/rest)                                                 | Datastream — Serverless Change Data Capture (CDC) and replication tool for streaming DB updates.                                            |
| [deploymentmanager.googleapis.com](https://docs.cloud.google.com/deployment-manager/docs/apis)                                            | Deployment Manager — Infrastructure-as-code tool deploying GCP resources using YAML templates.                                              |
| [dialogflow.googleapis.com](https://docs.cloud.google.com/dialogflow/es/docs/reference/rest/v2-overview)                                  | Dialogflow — Builds conversational interfaces, virtual agents, and chatbots powered by generative AI.                                       |
| [discoveryengine.googleapis.com](https://docs.cloud.google.com/generative-ai-app-builder/docs/reference/rest)                             | Vertex AI Search and Conversation — Generative AI search and discovery engine for enterprise data.                                          |
| [dlp.googleapis.com](https://docs.cloud.google.com/sensitive-data-protection/docs/reference/rpc)                                          | Cloud Data Loss Prevention — Inspects, classifies, and anonymizes sensitive data like PII and credit card numbers.                          |
| [dns.googleapis.com](https://docs.cloud.google.com/dns/docs/reference/rest)                                                               | Cloud DNS — Reliable, low-latency Domain Name System (DNS) service for domain management.                                                   |
| [documentai.googleapis.com](https://docs.cloud.google.com/document-ai/docs/reference/rest?rep_location=global)                            | Document AI — Extracts structured fields and text from unstructured documents (PDFs, forms, invoices).                                      |
| [domains.googleapis.com](https://docs.cloud.google.com/domains/docs/reference/rest)                                                       | Cloud Domains — Registers, transfers, and manages custom domain names within Google Cloud.                                                  |
| [essentialcontacts.googleapis.com](https://docs.cloud.google.com/resource-manager/docs/reference/essentialcontacts/rest)                  | Essential Contacts — Manages administrative points of contact for automated Google system notifications.                                    |
| [eventarc.googleapis.com](https://docs.cloud.google.com/eventarc/docs/reference/rest?rep_location=global)                                 | Eventarc — Routes asynchronous events from GCP sources or custom services to target endpoints.                                              |
| [file.googleapis.com](https://docs.cloud.google.com/filestore/docs/reference/rest)                                                        | Filestore — Fully managed Network Attached Storage (NAS) providing shared file systems (NFS) for applications.                              |
| [firebaseappdistribution.googleapis.com](https://firebase.google.com/docs/reference/app-distribution/rest)                                | Firebase App Distribution — Releases pre-release builds of iOS and Android apps directly to beta testers.                                   |
| [firebasedatabase.googleapis.com](https://firebase.google.com/docs/reference/rest/database/database-management/rest)                      | Firebase Realtime Database — Real-time NoSQL database syncing data across connected mobile and web clients.                                 |
| [firebasehosting.googleapis.com](https://firebase.google.com/docs/reference/hosting/rest)                                                 | Firebase Hosting — Fast, secure static and dynamic web content delivery across a global CDN.                                                |
| [firebaseremoteconfig.googleapis.com](https://firebase.google.com/docs/reference/remote-config/rest)                                      | Firebase Remote Config — Modifies application behavior and appearance dynamically without releasing app store updates.                      |
| [firebaserules.googleapis.com](https://firebase.google.com/docs/reference/rules/rest)                                                     | Firebase Security Rules — Configures authorization and input validation rules for Firebase databases and cloud storage.                     |
| [firestore.googleapis.com](https://docs.cloud.google.com/firestore/docs/reference/rest?rep_location=global)                               | Cloud Firestore — Flexible, scalable NoSQL document database built for real-time mobile and web app syncing.                                |
| [gkebackup.googleapis.com](https://docs.cloud.google.com/kubernetes-engine/docs/add-on/backup-for-gke/reference/rest?rep_location=global) | Backup for GKE — Automates backing up and restoring Kubernetes workloads and persistent volume data.                                        |
| [gkehub.googleapis.com](https://docs.cloud.google.com/kubernetes-engine/fleet-management/docs/reference/rest)                             | GKE Fleet Management — Manages multiple Kubernetes clusters as unified fleets across hybrid and multi-cloud platforms.                      |
| [healthcare.googleapis.com](https://docs.cloud.google.com/healthcare-api/docs/reference/rest)                                             | Cloud Healthcare API — Stores and exchanges healthcare data using FHIR, DICOM, and HL7v2 standards.                                         |
| [iap.googleapis.com](https://docs.cloud.google.com/iap/docs/reference/rest)                                                               | Identity-Aware Proxy — Grants context-aware access to web apps and VMs without needing a traditional VPN.                                   |
| [identitytoolkit.googleapis.com](https://docs.cloud.google.com/identity-platform/docs/reference/rest)                                     | Identity Platform — Manages user authentication, multi-factor authentication, and identity federations for apps.                            |
| [integrations.googleapis.com](https://docs.cloud.google.com/application-integration/docs/reference/rest)                                  | Application Integration — Enterprise Integration Platform as a Service (iPaaS) for connecting apps without custom code.                     |
| [looker.googleapis.com](https://docs.cloud.google.com/looker/docs/reference/rest)                                                         | Looker — Business intelligence and data platform for visualizing and analyzing data across platforms.                                       |
| [managedidentities.googleapis.com](https://docs.cloud.google.com/managed-microsoft-ad/reference/rest)                                     | Managed Microsoft AD — Provides fully managed Microsoft Active Directory infrastructure on GCP.                                             |
| [managedkafka.googleapis.com](https://docs.cloud.google.com/managed-service-for-apache-kafka/docs/reference/rest)                         | Managed Service for Apache Kafka — Fully managed streaming platform for Apache Kafka event workloads.                                       |
| [memcache.googleapis.com](https://docs.cloud.google.com/memorystore/docs/memcached/reference/rest)                                        | Memorystore for Memcached — Managed, scalable in-memory key-value caching service.                                                          |
| [metastore.googleapis.com](https://docs.cloud.google.com/dataproc-metastore/docs/reference/rest)                                          | Dataproc Metastore — Fully managed Apache Hive metastore for tracking big data lake schemas.                                                |
| [ml.googleapis.com](https://docs.cloud.google.com/workflows/docs/reference/googleapis/ml/Overview)                                        | AI Platform (Legacy) — Legacy machine learning service for training and hosting predictive models.                                          |
| [monitoring.googleapis.com](https://docs.cloud.google.com/monitoring/api/ref_v3/rest)                                                     | Cloud Monitoring — Tracks infrastructure performance metrics, uptime checks, dashboards, and operational alerts.                            |
| [netapp.googleapis.com](https://docs.cloud.google.com/netapp/volumes/docs/reference/rest?rep_location=global)                             | NetApp Volumes — High-performance, fully managed NFS and SMB file storage service.                                                          |
| [networkconnectivity.googleapis.com](https://docs.cloud.google.com/network-connectivity/docs/reference/networkconnectivity/rest)          | Network Connectivity Center — Orchestrates multi-cloud and hybrid cloud networking using Google's global network backbone.                  |
| [networksecurity.googleapis.com](https://docs.cloud.google.com/network-security-integration/docs/reference/rest)                          | Network Security API — Configures advanced network security rules, Cloud NGFW policies, and threat prevention.                              |
| [networkservices.googleapis.com](https://docs.cloud.google.com/service-extensions/docs/reference/rest)                                    | Network Services — Configures traffic management, Service Mesh, and custom network extensions.                                              |
| [notebooks.googleapis.com](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest)             | Vertex AI Workbench / Notebooks — Deploys managed Jupyter notebook environments for data science workflows.                                 |
| [orgpolicy.googleapis.com](https://docs.cloud.google.com/organization-policy/reference/rest)                                              | Organization Policy API — Sets centralized guardrails and restrictions across Google Cloud organization hierarchies.                        |
| [osconfig.googleapis.com](https://docs.cloud.google.com/compute/docs/osconfig/rest)                                                       | VM Manager / OS Config — Manages operating system patches, configuration management, and software licenses on compute instances.            |
| [policyanalyzer.googleapis.com](https://docs.cloud.google.com/policy-intelligence/docs/reference/policyanalyzer/rest)                     | Policy Analyzer — Analyzes and audits IAM policies to discover access risks and permission paths.                                           |
| [privateca.googleapis.com](https://docs.cloud.google.com/certificate-authority-service/docs/reference/rest)                               | Certificate Authority Service — Simplifies creation and management of private Public Key Infrastructure (PKI) CAs.                          |
| [recaptchaenterprise.googleapis.com](https://docs.cloud.google.com/recaptcha/docs/reference/rest)                                         | reCAPTCHA Enterprise — Protects web apps from bots, fraud, credential stuffing, and scraping attacks.                                       |
| [recommender.googleapis.com](https://docs.cloud.google.com/recommender/docs/reference/rest)                                               | Recommender API — Delivers automated recommendations for security, cost optimization, and performance.                                      |
| [redis.googleapis.com](https://docs.cloud.google.com/memorystore/docs/redis/reference/rest)                                               | Memorystore for Redis — Fully managed in-memory data store for caching and sub-millisecond data retrieval.                                  |
| [run.googleapis.com](https://docs.cloud.google.com/run/docs/reference/rest)                                                               | Cloud Run — Executes stateless containerized applications on a fully managed serverless platform.                                           |
| [secretmanager.googleapis.com](https://docs.cloud.google.com/secret-manager/docs/reference/rest?rep_location=me-central2)                 | Secret Manager — Centralized storage for sensitive values like passwords, tokens, API keys, and certificates.                               |
| [securitycenter.googleapis.com](https://docs.cloud.google.com/security-command-center/docs/reference/rest?rep_location=global)            | Security Command Center — Centralized security posture management, risk evaluation, and threat detection.                                   |
| [servicedirectory.googleapis.com](https://docs.cloud.google.com/service-directory/docs/reference/rest)                                    | Service Directory — Single catalog for discovering, registering, and resolving network services.                                            |
| [servicemanagement.googleapis.com](https://docs.cloud.google.com/service-infrastructure/docs/service-management/reference/rest)           | Service Management API — Manages service deployment specifications and API configuration settings across GCP.                               |
| [sourcerepo.googleapis.com](https://docs.cloud.google.com/source-repositories/docs/reference/rest)                                        | Cloud Source Repositories — Hosted, private Git repositories with built-in integrations.                                                    |
| [spanner.googleapis.com](https://docs.cloud.google.com/spanner/docs/reference/rest?rep_location=global)                                   | Cloud Spanner — Globally distributed, horizontally scalable relational database with transactional consistency.                             |
| [speech.googleapis.com](https://docs.cloud.google.com/speech-to-text/docs/reference/rest)                                                 | Speech-to-Text — Converts audio into written text using speech recognition models.                                                          |
| [sqladmin.googleapis.com](https://docs.cloud.google.com/sql/docs/postgres/admin-api/rest)                                                 | Cloud SQL Admin — Provisions and manages relational database instances (MySQL, PostgreSQL, SQL Server).                                     |
| [storagetransfer.googleapis.com](https://docs.cloud.google.com/storage-transfer/docs/reference/rest)                                      | Storage Transfer Service — Moves bulk data quickly between cloud providers (AWS, Azure) or local storage to GCP.                            |
| [tpu.googleapis.com](https://docs.cloud.google.com/tpu/docs/reference/rest)                                                               | Cloud TPU — Provides Tensor Processing Unit hardware accelerators optimized for deep learning models.                                       |
| [translate.googleapis.com](https://docs.cloud.google.com/translate/docs/reference/rest)                                                   | Cloud Translation — Translates text into over 100 languages dynamically using Google ML models.                                             |
| [vmwareengine.googleapis.com](https://docs.cloud.google.com/vmware-engine/docs/reference/rest)                                            | Google Cloud VMware Engine — Migrates and runs native VMware vSphere workloads directly on dedicated GCP hardware.                          |
| [vpcaccess.googleapis.com](https://docs.cloud.google.com/vpc/docs/reference/vpcaccess/rest)                                               | Serverless VPC Access — Enables serverless environments (Cloud Run, Functions) to connect privately to internal VPC resources.              |
| [websecurityscanner.googleapis.com](https://docs.cloud.google.com/security-command-center/docs/reference/web-security-scanner/rest)       | Web Security Scanner — Crawls and identifies common web security vulnerabilities in compute and App Engine apps.                            |
| [workflows.googleapis.com](https://docs.cloud.google.com/workflows/docs/reference/rest)                                                   | Workflows — Links and orchestrates multiple cloud APIs and HTTP endpoints into serverless workflows.                                        |
| [workstations.googleapis.com](https://docs.cloud.google.com/workstations/docs/reference/rest)                                             | Cloud Workstations — Managed cloud-based development environments for developer security and standardization.                               |

#### APIs required by specific security capabilities

If you enable any of the following Cortex XSIAM capabilities, the listed APIs must be enabled on every scanned project that holds the relevant resources. These are in addition to the core APIs, not a replacement for them.

| Capability                              | APIs required on scanned projects                                                                              |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Agentless Disk Scanning                 | `compute.googleapis.com`                                                                                       |
| Data Security Posture Management (DSPM) | `bigquery.googleapis.com`, `bigtableadmin.googleapis.com`, `sqladmin.googleapis.com`, `storage.googleapis.com` |
| Registry Scanning                       | `artifactregistry.googleapis.com`                                                                              |
| Serverless Scanning                     | `cloudfunctions.googleapis.com`, `storage.googleapis.com`                                                      |

#### Enable the APIs on the service account project <a href="#enable-the-apis-on-the-service-account-project" id="enable-the-apis-on-the-service-account-project"></a>

Run the following against the project that hosts the Cortex XSIAM service account:

```bash
gcloud services enable \
  cloudasset.googleapis.com \
  cloudresourcemanager.googleapis.com \
  serviceusage.googleapis.com \
  iam.googleapis.com \
  logging.googleapis.com \
  pubsub.googleapis.com \
  storage.googleapis.com \
  --project <SERVICE_ACCOUNT_PROJECT_ID>
```

#### Enable the core APIs on every scanned project <a href="#enable-the-core-apis-on-every-scanned-project" id="enable-the-core-apis-on-every-scanned-project"></a>

For an organization or folder onboarding, repeat the core API enablement across every project in scope:

```bash
for PROJECT in $(gcloud projects list --format="value(projectId)"); do
  gcloud services enable \
    cloudasset.googleapis.com \
    cloudresourcemanager.googleapis.com \
    serviceusage.googleapis.com \
    iam.googleapis.com \
    --project "$PROJECT"
done
```

Note: `gcloud projects list` returns every project your credentials can see. Filter the list to match the organization or folder you are onboarding if your access spans more than one scope.

#### Verify what is enabled <a href="#verify-what-is-enabled" id="verify-what-is-enabled"></a>

Confirm the result on any individual project:

```bash
gcloud services list --enabled --project <PROJECT_ID>
```

To find projects that are still missing the Cloud Asset API, which is the most common gap after an organization onboarding:

```bash
for PROJECT in $(gcloud projects list --format="value(projectId)"); do
  if ! gcloud services list --enabled --project "$PROJECT" \
       --filter="config.name:cloudasset.googleapis.com" --format="value(config.name)" | grep -q .; then
    echo "Missing cloudasset.googleapis.com: $PROJECT"
  fi
done
```

### Ongoing maintenance <a href="#ongoing-maintenance" id="ongoing-maintenance"></a>

New projects created inside an onboarded organization or folder do not inherit enabled APIs. Each newly created project starts with the core APIs disabled, and its assets stay invisible to Cortex XSIAM until you enable them.

If your organization creates projects regularly, enforce API enablement as part of your project provisioning process, for example through a project factory Terraform module, Config Controller, or another bootstrap mechanism that enables the core APIs on every new project.<br>
