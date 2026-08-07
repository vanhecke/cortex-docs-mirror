# Manage autonomous playbooks

While autonomous playbooks execute complex security operations, they provide a streamlined user experience. Autonomous playbooks are automatically updated and cannot be edited, duplicated, deleted, or downloaded. You can view the high-level structure of the playbook and enable or disable it.

Autonomous playbooks appear in the **Playbooks** page with the autonomous playbooks <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-96ae5afbb583e4d6d3843869864ee439899cc702%2F7644a553964b8650418c3544b0a626192059534222543366909c85c703902d44.png?alt=media" alt="autonomous_playbook_icon.png" data-size="line"> icon. You can filter the Org repository table to view only autonomous playbooks.

Autonomous playbooks do not appear in the **Playbook Catalog**, and you cannot execute autonomous playbooks via the command line, run them as sub-playbooks, or assign them to be triggered by custom automation rules. Autonomous playbooks are only triggered by autonomous automation rules.

To view the high-level visual structure of an autonomous playbook, click the playbook name in the **Playbooks** page. You can view the automation rules that trigger the playbook as well as the **Potential Response,** which lists the important commands and scripts. Tasks that require manual user approval have a dedicated flag <img src="https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-acf666b6ff49bd53887f6e9dfd17fe14cf239410%2F1181f02cb297d400daf033b8b0e923e1a356df0472c62169bcd1aaabcfc48b31.png?alt=media" alt="manual_approval.png" data-size="line">. If a command or script is associated with an automation exclusion policy, the playbook provides a direct link to the policy in the **Automation Exclusion Center**.

If you need to temporarily stop a specific autonomous playbook from running, you can disable it. On the **Playbooks** page, right-click the autonomous playbook in the Org repository table and select **Disable**. To turn it back on, right-click it again and select **Enable**.

As new autonomous playbooks related to Cortex Analytics are released, they automatically appear in the **Playbooks** page. By default, they are enabled.
