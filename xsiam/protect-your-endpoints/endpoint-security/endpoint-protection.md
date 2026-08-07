---
description: >-
  This topic provides an overview of traditional endpoint protection versus the
  protection of endpoints using Cortex XSIAM.
---

# Endpoint protection

Cyberattacks target endpoints to inflict damage, steal information or achieve other goals that involve taking control of computer systems. Attackers perpetrate cyberattacks either by causing a user to unintentionally run a malicious executable file, known as malware, or by exploiting a weakness in a legitimate executable file to run malicious code behind the scenes without the knowledge of the user.

One way to prevent these attacks is to identify files, dynamic-link libraries (DLLs), and other pieces of code to determine if they are malicious and, if so, to prevent the execution of these components by first matching each potentially dangerous code module against a list of specific, known threat signatures. The weakness of this is that it is time-consuming for signature-based antivirus (AV) solutions to identify newly created threats that are known only to the attacker (also known as zero-day attacks or exploits) and add them to the lists of known threats, which leaves endpoints vulnerable until signatures are updated.

Cortex XSIAM takes a more efficient and effective approach to prevent attacks that eliminates the need for traditional AV. Rather than try to keep up with the ever-growing list of known threats, Cortex XSIAM sets up a series of roadblocks that prevent the attacks at their initial entry points, the point where legitimate executable files are about to unknowingly allow malicious access to the system.

Cortex XSIAM provides a multi-method protection solution with exploit protection modules that target software vulnerabilities in processes that open non-executable files and malware protection modules that examine executable files, DLLs, and macros for malicious signatures and behavior. Using this multi-method approach, along with AI analysis Cortex XSIAM can prevent all types of attacks, whether these are known or unknown threats.

![cortex-xdr-multi-method-prevention.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-33e525a91963a6583ec23f05f31a199900a6913d%2F08289a729eca57174ccf16fc176f9352eb8ecf2e7f1e3a048e4e17fd91111397.png?alt=media)
