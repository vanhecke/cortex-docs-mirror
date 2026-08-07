---
description: Configure integration commands that retrieve reputation data for indicators.
---

# Reputation commands

Reputation commands are built-in or custom commands that use integrations to provide predefined functionalities for obtaining an indicator verdict for specific indicator types. These commands simplify the process of fetching reputation data from external services or threat intelligence feeds without requiring extensive scripting. Reputation commands come with preconfigured parameters and settings for commonly used threat intelligence sources.

You can set an indicator type to run reputation commands. The command returns the verdict of the indicator as an entry with entry context and may also return context values that can be mapped to the custom fields of the indicator.

{% hint style="info" %}
### Note

Running a reputation command directly (such as `!ip`) might not apply the result to an indicator, nor does it use the enrichment cache. To ensure an indicator is enriched, and to take advantage of caching, use the `enrichIndicators` command or the **Enrich** button in the UI. This runs the appropriate reputation command/script based on the indicator type settings. Note that extracted indicators are enriched in the same way.
{% endhint %}

Out-of-the-box reputation commands

You can create a new reputation command, or you can use an out-of-the-box reputation command, for example:

* `ip`
* `file`
* `url`
* `email`
* `domain`

For more details on using out-of-the-box reputation commands or developing new reputation commands, see [Generic Reputation Commands](https://xsoar.pan.dev/docs/integrations/generic-commands-reputation).

**Reputation command input**

The reputation command uses the indicator value as the input argument.

| Arguments                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The value of the indicator | <p>For example <strong><code>ip</code></strong>, <strong><code>email</code></strong>, <strong><code>url</code></strong>. Inputs are based on different integrations. Basic inputs are common to all reputation commands. For example, the <strong><code>!ip</code></strong> command has the following basic inputs:</p><p><code>- name: ip arguments: - name: ip default: true description: List of IPs. isArray: true</code></p> |

In this example, the **`ip`** script uses **`ip`** as the input, with **`is array`** unchecked.

![ip-script-8.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-ef92747a6f5c13f403ea63b7328b8ae4bd113c7b%2Fb65d050b2daed0fb5f557329f0d60e89290d77a423c3bb169d6fcc8ceb37e74a.png?alt=media)

**Reputation command output**

Outputs return a [dbotScore](https://xsoar.pan.dev/docs/integrations/dbot).

**Run a Reputation command in the CLI**

The following are examples of the syntax for running the `ip` , `domain`, and `file` reputation commands in the CLI.

* `!ip ip=<indicator IP>`
* `!domain domain=<indicator domain>`
* `!file file=<indicator file hash>`
* `!file file=<indicator file hash> using=<a specific integration instance>`
