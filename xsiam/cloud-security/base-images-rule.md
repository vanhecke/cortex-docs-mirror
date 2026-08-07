# Base image rules

A **Base Images** rule defines which registry images your organization considers foundational base images and maps derived images to them. This association provides image lineage visibility, helping you trace vulnerabilities to their source and apply remediation at the base image level.

A **Base Images** rule associates registry images (for example, ubuntu:22.04) as designated base images. When a rule is applied, it creates a **BASE\_REFERENCE** relation between images, enabling bidirectional tracing so you can:

* Identify the base image for any given image
* View all dependent images derived from a specific base image

By creating **Base Images** rule, you can:

* Identify approved base images across your organization
* Map Registry and Runtime images to base images for full lineage visibility
* Identify affected base images during vulnerability investigations
* Identify all dependent images impacted by a vulnerable base image
* Use base image associations in policies, queries, and filters
