---
description: Cortex XSIAM parameter types for integration instances and scripts.
---

# Integration and script parameter types

Integration parameter types are used for configuring integration instances. When adding a parameter to an integration in Cortex XSIAM, you assign it a type. The parameter type affects the parameter behavior and interaction with the user. See Configuration in the [Integration metadata YAML file](integration-metadata-yaml-file) for more information about how to set the parameter type.

### Boolean integration parameter type

This parameter type creates a checkbox in the integration instance settings configuration in the UI. When the checkbox is checked, the value in the integration code is True. If the checkbox is not checked, the value is False.

The type number is 8.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-7015c7cc8975c3ed34445199ad8ad2ab0e36fcb2%2Fa5a61e1918260e7852f80566dd2845389883e094c10c8800a851fcb9c8ef9eb0.png?alt=media)

Access: `demisto.params().get('proxy')`

### Short text integration parameter type

This parameter type is used for short input parameters, such as server URLs, ports or queries. It creates a small text box in the integration instance settings configuration in the UI.

The type number is 0.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-a93e4134f2484912ef73b353b7be9fea03605292%2F689a96dcdc50995b97489cc4771fb2e180f874d7c27ecdb373a8fdf8598925ba.png?alt=media)

Access: `demisto.params().get('url')`

### Long text integration parameter type

This parameter type is used for long text inputs, such as certificates. It creates a large text box in the integration instance settings configuration in the UI.

The type number is 12.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-ce2128ce2bf2c773e9d6bf8272ac7bd7e9c93921%2F84a92d673530b89429f12b21dff826c59980b8393d0fa48e3b8584aee445ec2a.png?alt=media)

Access: `demisto.params().get('cert')`

### Short encrypted integration parameter type

This parameter type is used for encrypted inputs, such as API tokens. This should not be used for username/password credentials. It creates a small text box for encrypted text, which is also stored encrypted in the database.

The type number is 4.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-fcb3e36ff617b8d53eb8ebacd7ba177a6e9830b8%2Fff3d9cacf60683cbcfaff6b0c79ed85d218509f6fbf690cd401fe6ecb99b9098.png?alt=media)

Access: `demisto.params().get('token')`

### Long encrypted integration parameter type

This type of parameter is used for long encrypted inputs, such as certificates. It creates a text area with encrypted text. The text is also stored encrypted in the database.

The type number is: 14.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-9cfabb8b1775e9d2ed079a3bdf21ce5b1375dd16%2F84d388e6956c1c6d634c3ee805b3311d7e563ca61e7326f3d942768e6352e560.png?alt=media)

Access: `demisto.params().get('cert')`

### Authentication integration parameter type

This parameter type is used for username/password credentials, with plain text username and an encrypted password. It supports retrieving credentials from the Cortex XSIAM credentials store (see the Cortex XSIAM support portal for more about the credentials store).

The type number is 9.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-a21ce1bfb893426519799ab388e5920cb8d8165b%2F948538ab019fa8a52f94998b3085fd64b943dfbe1603a76e19c4ef9734ed998d.png?alt=media)

Access:

* Username: `demisto.params().get('credentials', {}).get('identifier')`
* Password: `demisto.params().get('credentials', {}).get('password')`

### Single-select integration parameter type

This parameter type enables selecting a single input from a list of allowed inputs.

The type number is 15.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-335e0d2b555a7a878988cedf2b6b79b40c949abb%2Fc01a8a35be5098845a20440222745d39434341b47799d4e86326e4d7815ad196.png?alt=media)

Access: `demisto.params().get('log')`

### Multi-select integration parameter type

This parameter type enables selecting multiple inputs from a list of allowed inputs.

The type number is 16.

![](https://4088726609-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FurXrv6qkJRLbdhMdvPIU%2Fuploads%2Fgit-blob-c0b83f6ab1bbbb132de206f4c979f4ff7af6779e%2Fc49c824cd31246eb306d9df06dc04030697c0da7d39754193c67b90e02b2a28b.png?alt=media)

Access: `demisto.params().get('sort')`

### Maintain integration parameter compatibility

Once a parameter is set in an integration instance settings configuration, it is saved to the Cortex XSIAM database. Before changing an existing parameter, consider the existing values to ensure backward compatibility. For example, when adding a parameter with a default value to an existing integration, add the default value in the code as well as the YAML file, as it is not added to existing instances.
