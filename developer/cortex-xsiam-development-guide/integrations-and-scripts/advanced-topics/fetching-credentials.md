---
description: >-
  Integrate with third-party credential vaults for Cortex XSIAM to authenticate
  with integrations.
---

# Fetching credentials

You can integrate with [third-party credential vaults](https://app.gitbook.com/s/AEIjuYE3RXcIfmuQnBbm/) for Cortex XSIAM to use when authenticating with integrations. This topic provides an example of a vault integration.

### Credential vault integration requirements

To fetch credentials to the Cortex XSIAM credentials store, the vault integration needs to retrieve credential objects in the format of a username and password `(key:value)`.

### Implement credential fetching

#### Configure the `isFetchCredentials` parameter

For this example we look at the **HashiCorp Vault** integration. The integration contains a Boolean parameter called `isFetchCredentials`. When this parameter is set to `true`, Cortex XSIAM fetches credentials from the vault integration.

![hashicorp-parameter.png](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-7b0fefb07b8215ffcd019b16b3405375a594aa04%2F794ce8d20cc091d98ace0e6e9cf4a1d38deae947d256795a3a400aebc2d70c0d.png?alt=media)

When you configure an instance of this integration, the parameter appears:

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-8970387f62521b2146a3d69065a0563b1fc4e886%2F08e2f962890f957e33f8abdcccc2a93b28caa32e2b41543bc0f522ab3c1993cf.png?alt=media)

#### Implement the `fetch-credentials` command

When Cortex XSIAM fetches credentials from vault integrations, it calls a command called `fetch-credentials`. This is where you implement the credentials retrieving logic:

```programlisting
if demisto.command() == 'fetch-credentials':
   fetch_credentials()
```

In the `fetch_credentials` function, you retrieve the credentials from the vault and create new JSON objects in the format:

```programlisting
{
  "user": "username",
  "password": "password",
  "name": "name"
}
```

You should now have a credentials list that contains the above objects.

```programlisting
[
  {
    "user": "username_foo",
    "password": "password_foo",
    "name": "name_foo"
  },
  {
    "user": "username_bar",
    "password": "password_bar",
    "name": "name_bar"
  }
]
```

When you're done creating the credentials objects, send them to the credentials store:

```programlisting
demisto.credentials(credentials)
```

With the `fetch_credentials` command, you can either fetch all credentials or fetch a specific set of credentials.

#### Fetch all vault credentials

To have all relevant credentials from a vault integration visible and usable in other integrations, the `fetch-credentials` command needs to support the logic of pulling multiple credentials. We recommend creating a dedicated parameter in the vault integration which allows the user to specify which credentials should be pulled. For our example, we name this parameter `credential_names`:

```programlisting
params: dict = demisto.params()
credentials_str = params.get('credential_names')
credentials_names_from_configuration = argToList(credentials_str)  # argToList is a wrapper to safely execute the str.split() function
credentials = []
for credentials_name in credentials_names_from_configuration:
    credentials.append(get_credentials(credentials_name))

demisto.credentials(credentials)
```

You can now see the credentials in the Cortex XSIAM credentials store, found at **Settings** → **Configurations** → **Integrations** → **Credentials**.

These credentials cannot be edited or deleted, they reflect exactly what's in the vault. You can stop fetching credentials by clearing the **Fetch Credentials** checkbox in the integration settings.

#### Fetch specific vault credentials

A user might choose to configure another integration using a set of credentials fetched by a vault integration:

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-1e753263f4eca594d6b4e182a48f97431c00833a%2Fc9a02f98051062ad6655ed6d6c33e29a12d1f7516c677f821decdd33edee801d.png?alt=media)

Since Cortex XSIAM does not store the credentials in its database, each time these credentials are used in the new configured integration, Cortex XSIAM queries the vault integration for it. To extract the specific credentials name use the identifier argument stored in `demisto.args()`:

```programlisting
args: dict = demisto.args()
credentials_name: str = args.get('identifier')
try:
    credentials: list = [get_credentials(credentials_name)]
except Exception as e:
    demisto.debug(f"Could not fetch credentials: {creds_name}. Error: {e}")
    credentials = []

demisto.credentials(credentials)
```

{% hint style="info" %}
**Important**

When working with a specific credentials name (the identifier key), always return a list containing up to one set of credentials. It is important to catch errors that are part of this flow, and instead of raising them, return an empty list. If no list or a list with more than one element is returned, the credentials tab will fail to load.
{% endhint %}

Both options together:

```programlisting
params: dict = demisto.params()
args: dict = demisto.args()
credentials_str = params.get('credential_names')
credentials_names_from_configuration = argToList(credentials_str)  # argToList is a wrapper to safely execute the str.split() function
credentials_name: str = args.get('identifier')
if credentials_name:
    try:
        credentials: list = [get_credentials(credentials_name)]
    except Exception as e:
        demisto.debug(f"Could not fetch credentials: {creds_name}. Error: {e}")
        credentials = []
else:
    credentials = []
    for credentials_name in credentials_names_from_configuration:
        credentials.append(get_credentials(credentials_name))

demisto.credentials(credentials)
```

### Troubleshoot credential fetching

* If there is an error during the process, you can debug your code by adding a test command that calls the `fetch_credentials` function. Send a credentials list in the right format and as a valid JSON.
* To save API calls every time a credential is used, Cortex XSIAM uses a short time caching mechanism for fetched credentials. This can cause issues when you are trying to debug fetching a specific set of credentials.
