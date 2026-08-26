# Self-service API keys for CLI scans

This self-service model uses a Primary API key as its master credential. It lets developers programmatically generate task-specific CLI and IDE keys through the Public API. Developers can provision restricted-access keys, such as `read-only` keys for local scans, without administrative UI permissions. This keeps each scan within the principle of least privilege.

## Prerequisite

You must have sufficient administrative permissions within your tenant to create new roles and manage API keys.

**IMPORTANT**: When generating an API key, ensure you select the Standard security level. CLI scans will fail if the security level of the API key is set to Advanced.

## Create custom roles

Navigate to your role management settings in the tenant to generate the following three roles with these exact permission sets.

| Role name              | Required permission and description                                                                                          |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| CLI Read-Only Custom   | **CLI Tools View**: Grants permission to run CLI scans and view output locally without uploading results to the tenant       |
| CLI Write Custom       | **CLI Tools View/Edit**: Grants permission to run CLI scans and upload/manage results within the tenant                      |
| Public API (PAPI) Edit | **Public API View/Edit**: Grants the administrative permission required to programmatically generate and manage new API keys |

## Assign roles to a privileged user

To establish a Primary key holder, you must grant a specific privileged user the permissions from all three custom roles. Because the UI allows only one role to be assigned directly to a user, you must use User Groups to grant multiple roles simultaneously.

1. **Create user groups**: Create three separate User Groups in your tenant, assigning one of the custom roles to each group.
2. **Add user to groups**: Add the designated privileged user to all three of these User Groups.
3. **Verify accumulated permissions**: Edit the primary user and ensure that the User Groups field includes the three user groups.

This user now has the combined authority to generate the Primary API Key required to set up programmatic key generation.

## Generate and use API keys

The designated privileged user must manually generate a Primary API Key through the console. This key must be associated with the `CLI Read-Only Custom`, `CLI Write Custom`, and `Public API (PAPI) Edit` roles. The primary key acts as the master credential for subsequent automation.

Using the Primary Key, developers can now make calls to the Public API to generate subsequent keys as needed for IDE or CLI scans:

* To run scans without uploading the results to the platform: Generate a key and associate it only with the `CLI Read-Only Custom` role.
* To run scans and upload the results to the platform: Generate a key and associate it only with the `CLI Write Custom` role.

The following `curl` command demonstrates how developers can use the Primary Key to generate a new API key assigned with the `CLI Read-Only Custom` role:

```programlisting
 curl --request POST \
  --url https://api-viso-k2ibu8behynsxbzuncdau6.xdr-qa2-uat.us.paloaltonetworks.com/public_api/v1/api_keys/generate \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --header 'authorization: <YOUR_PRIMARY_KEY_HERE>' \
  --header 'x-xdr-auth-id: <YOUR_AUTH_ID>' \
  --data '{
  "request_data": {
    "roles": [
      "CLI Read-Only Custom"
    ],
    "security_level": "standard",
    "comment": "Developer CLI Read-Only scan key",
    "expiration": 1773147108
  }
}'
```

For more information about generating API Keys, refer to [Manage API keys](../../../learn-about-cortex-xsiam/manage-api-keys).

To ensure the keys are configured correctly, privileged users can verify their status by navigating to **Settings** → **API Keys**. Locate the generated key in the API Keys inventory and confirm that the Role column reflects the specific custom role assigned rather than a broad administrative role.
