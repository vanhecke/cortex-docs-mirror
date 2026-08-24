---
description: Configure custom certificates for secure Cortex XSIAM engine communication.
---

# Configure an engine to use custom certificates

You can replace the default self-signed certificate for the engine with your own certificate.

1.  Find the two files created by the engine. The default location is **`/usr/local/demisto`**.

    **`d1.key.pem`**

    **`d1.cert.pem`**
2. Replace the contents of these files with your own certificates.
3.  Change file owner to demisto:

    **`chown -R demisto:demisto d1.key.pem`**

    **`chown -R demisto:demisto d1.cert.pem`**
4.  Set the file permissions:

    **`chmod 600 d1.key.pem`**

    **`chmod 644 d1.cert.pem`**
