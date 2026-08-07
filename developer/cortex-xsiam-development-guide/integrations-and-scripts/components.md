---
description: >-
  Learn about integration and script directory structure, metadata YAML file,
  parameter types, integration description file, integration logo standards, and
  README file.
---

# Components

Integrations and scripts in Cortex XSIAM are stored in YAML files that include all the required information (metadata, code, images, etc.). All these files together are referred to as a Unified YAML file.

To better handle the files in the content repository, Python/Powershell scripts and integrations are stored in a directory structure, where the YAML files only contain the metadata and the code and artifacts live in separate files. This is required for running linting and unit testing of the code.

When an integration or script is exported from Cortex XSIAM using `demisto-sdk download`, the Unified YAML is automatically split into its components. When other components (such as playbooks, alert fields, and layouts) are downloaded, they are exported as is and automatically added to their respective folders.

When an integration or script is imported into Cortex XSIAM using **demisto-sdk upload**, the integration/script directory files are automatically assembled in the Unified YAML file that is uploaded.

Content developers usually work with the directory structure and not the unified file.
