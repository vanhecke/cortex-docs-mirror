---
description: >-
  Salesforce Automation and Remediation commands for playbooks and the War Room
  for Cortex XSIAM.
---

# Automation and remediation commands

If you selected the Automation and Remediation capability and the wizard configuration is complete and the connection is established, you can use the following commands in your playbooks or the War Room:

* General Salesforce and record operations
  * `salesforce-search-records`: Search for specific Salesforce records.
  * `salesforce-get-object` / `salesforce-create-object`: Read or create Salesforce objects.
  * `salesforce-get-org`: Returns organization details based on a case number.
* Case management
  * `salesforce-create-case`: Create a new case using a subject and status.
  * `salesforce-get-case` / `salesforce-get-case-information`: Retrieve detailed information about a specific case.
  * `salesforce-post-casecomment` / `salesforce-get-casecomment`: Post or return comments on a specific case.
* Chatter operations
  * `salesforce-add-comment-to-chatter`: Add a comment or link to a Chatter subject.
  * `salesforce-push-comment-threads`: Add a comment directly to a specific Chatter thread.
* Identity and Access Management (IAM) operations
  * `iam-create-user`: Create a new active user profile.
  * `iam-update-user`: Update existing user profile data.
  * `iam-get-user`: Retrieve a single user resource via identifier or case number.
  * `iam-disable-user`: Disable an active employee user profile - Security Posture: (Cloud Posture license only) Enables detecting, monitoring, and alerting on your cloud application settings.
