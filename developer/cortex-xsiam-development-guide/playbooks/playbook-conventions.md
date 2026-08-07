---
description: Recommendations for playbook and task naming, as well as playbook design tips.
---

# Playbook conventions

When creating playbooks to contribute, you need to following conventions and standards that keep playbooks consistent, usable, and readable.

#### Naming

* Names are Title Case.
*   Playbook names cannot contain the following special characters:

    ```programlisting
    Punctuation marks: ! " # $ % & ' ( ) * + , . / : ; < = > ? @ [ \ ] ^ ` { | } ~    
    Symbols: © ® ™ ° µ ± ß    
    Formatting characters: ¶ §
    ```
*   After the playbook name, but before specifying a version number or integration name, use a dash (-).

    Example: `Endpoint Enrichment - Generic v2`.
*   If adding `Test` to the playbook name, use a dash and add it to the end of the name.

    Example: `Phishing - Core - Test`
*   When adding `test` to a later version of a playbook, use `- Test` at the end.

    Example: `Phishing - Core v2 - Test`
*   In the descriptions of playbooks, specify the supported integrations or file types. File types are in capital letters. Integration names are in title case.

    ![integration\_names.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-97f1a398105afbbf6520e2b91ba697105ce05a72%2Fdee9685b68cd52cf87d462f316d52a4c87d287fe77c548dd665eb862c3cbf294.png?alt=media)

    ![filetypes.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-b38d473725d8937c94990b357db9f3249e1f05b1%2F184b003fdc8c45441dbf8fa41b4703ee989adbed279e58c3fad0ba95f6d176e2.png?alt=media)

#### Tasks

* The first letter of task names is capitalized. The rest of the task name is sentence case, but integration names should be capitalized.
* When using verbs, the verb form should be the simple command. For example, `Save`, and not `Saving` or `Saves`.
* Conditional tasks should end with a question mark. For example, `Is there a file?`, `Is there an endpoint to enrich?`, `Is there an email file attached?`, `Is Carbon Black Enterprise Response enabled?`,`Is there a Word file?`
* Descriptions of tasks, unlike the names of tasks, should use the verb form `Saves` and not `Save`. For example, `Checks if this is the first iteration`.

#### Tips

* To automatically extract indicators from an output of a command, in the task **Advanced** tab, select one of the options provided: **Use system default**, **None, Inline, Out of Band.** See [Indicator extraction](../indicators) for more information about each option.
* When outputting to context in integrations or scripts, use generic descriptions. For example, **Extract Indicators From File - Generic v2** has two different tasks outputting to `File.Text` but in the playbook outputs there is a description for only one.
* Set defaults for playbook inputs as needed, by clicking **Playbook Triggered** at the top of the playbook.
* Avoid programming terms, as playbooks can be used by non-programmers.
* When working with indicators or data that should be unique, use `Uniq` transformers to prevent duplications in the returned list. Do the same for playbook inputs.
* Avoid using [DT](../integrations-and-scripts/advanced-topics/transform-language-dt) (Transform Language) if not required. Instead, use selectors (**Get** step), filters, and transformers. This is easier to work with and also prevents a common error where data is passed by value instead of reference. An exception to this rule is when using the `Set` script, which sets a value to an output. You can not "get" that key, as it does not exist.
* Use the **Ignore case** option when checking user inputs, such as True/False in playbook inputs.
* Confirm task changes in all relevant sub-windows. Do not cancel, switch tasks, or navigate to another page, as your changes will not be saved.
* When editing a playbook that has a sub-playbook, if you changed the inputs/outputs of the sub-playbook, the changes are not reflected in the parent playbook, until you refresh the page. Saving the parent playbook and reopening the playbook may not show the changes until you refresh the page.

#### Visual Design

* When visually designing a playbook, the most important factor is to provide a clear understanding of the workflows, followed by overall readability, followed by general aesthetics.
* Group similar tasks.
* Align tasks/headers of the same level.
* Use section headers to split playbook tasks into different phases.
* Avoid headers as timer starts/stoppers.
