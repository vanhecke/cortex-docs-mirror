---
description: Cortex XSIAM integration directory structure and required files.
---

# Integration directory structure

Each integration is stored in the Integrations directory with a unique name, and includes the following file types:

```programlisting
 .
├── <INTEGRATION-NAME>.py              // Integration / automation script Python code.
├── <INTEGRATION-NAME>_test.py         // Python unit test code.
├── <INTEGRATION-NAME>.yml             // Configuration YAML file.
├── <INTEGRATION-NAME>_image.png       // Integration PNG logo (for integrations only).
├── <INTEGRATION-NAME>_description.md  // Detailed instructions markdown file (for integrations only)
├── README.md                          // Integration / automation script documentation.
```

For example, the Cortex XDR integration is stored in `Integrations/CortexXDRIR` and contains the following files:

```programlisting
.Integrations   
│
└─── .CortexXDRIR
│    ├── CortexXDRIR.py
│    ├── CortexXDRIR_test.py
│    ├── CortexXDRIR.yml
│    ├── CortexXDRIR_image.png
│    ├── CortexXDRIR_description.md
│    ├── README.md
```
