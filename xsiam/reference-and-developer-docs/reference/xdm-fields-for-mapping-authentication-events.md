---
description: >-
  Learn more about the Cortex Data Model (XDM) fields to map for authentication
  events.
---

# XDM fields for mapping authentication events

This section provides a comprehensive guide to mapping authentication events from various customer log sources to the XDM (Cortex Data Model) schema. Each relevant XDM field is detailed, including whether the field is mandatory or optional, the corresponding **Authentication Story** field , data type, and purpose, ensuring consistent data normalization essential for robust security analysis and threat detection.

The fields that are mandatory to map are listed below with an asterisk (\*) beside them as these fields must be mapped to automatically create authentication stories for XDM identity data.

{% hint style="info" %}
### Note

For more information on the entire Cortex Data model (XDM) schema, see [Cortex XSIAM Data Model Schema](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/).
{% endhint %}

## Mandatory fields

### 1. xdm.source.port\*

**Authentication Story Field**: `action_local_port`

**Type**: integer

**Requirement**: Mandatory

**Data Model Rule example**:

```programlisting
 xdm.source.port=to_integer(0)
```

### 2. xdm.target.ipv4\*

**Authentication Story Field**: `action_remote_ip`

**Type**: string

**Requirement**: Mandatory

**Note**: Map a field that isn't a String or list. If there is no relevant field to map to the target IP, populate this field with an empty string (`""`).

**Data Model Rule example**:

```programlisting
xdm.target.ipv4 = ""
```

### 3. xdm.target.port\*

**Authentication Story Field**: `action_remote_port`

**Type**: integer

**Requirement**: Mandatory

**Data Model Rule example**:

```programlisting
xdm.target.port=to_integer(0)
```

### 4. xdm.network.ip\_protocol\*

**Authentication Story Field**: `action_network_protocol`

**Type**: integer

**Requirement**: Mandatory

See full list of options for this enum in the [XDM IP Protocol documentation](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/consts/ip-protocol).

**Data Model Rule example**:

```programlisting
xdm.network.ip_protocol=XDM_CONST.IP_PROTOCOL_TCP
```

### 5. xdm.event.type\*

**Authentication Story Field**: `dfe_labels`

**Type**: string

**Requirement**: Mandatory

**Description**: Represents events related to authentication activity, such as login attempts, SSO sessions, and MFA challenges.

**Required Value**: Must contain `"authentication"`

**Data Model Rule example**:

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
xdm.event.type = if(eventType in ("user.authentication.sso", "user.session.start", "user.mfa.okta_verify.deny_push", "user.mfa.factor.update", "user.authentication.auth_via_mfa", "user.authentication.auth_via_AD_agent", "user.authentication.verify", "user.authentication.auth_via_radius", "user.authentication.auth_via_richclient", "system.push.send_factor_verify_push"), "authentication", "")
```
{% endcode %}

### 6. xdm.event.tags\*

**Authentication Story Field**: `dfe_labels`

**Type**: array\<string>

**Requirement**: Mandatory

**Description**: Represents events related to authentication activity, such as login attempts, SSO sessions, and MFA challenges.

**Required Value**: Must contain `XDM_CONST.EVENT_TAG_AUTHENTICATION`

**Data Model Rule example**:

```programlisting
xdm.event.tags = arraycreate(XDM_CONST.EVENT_TAG_AUTHENTICATION)
```

### 7. xdm.source.ipv4\*

**Authentication Story Field**: `action_local_ip`

**Type**: string

**Requirement**: Mandatory

**Description**: Represents the external IPv4 address from which the user authenticated. This is the IP address observed by the identity provider or SaaS system when the authentication request was processed. It typically reflects the user’s public-facing network location, such as their home IP, office gateway, or VPN egress point.

{% hint style="info" %}
### Note

Do not map a static string, list, or empty string. You must map this field from the raw log field that best represents the actual source IP used in the authentication attempt. In cases where multiple IP fields are available, such as `client_ip`, `source_ip`, and `original_client_ip`, choose the field that captures the IP address from which the user initially triggered the authentication request - before any processing by proxies or intermediate systems.
{% endhint %}

### 8. xdm.event.operation\*

**Authentication Story Field**: `event_sub_type`

**Type**: string

**Requirement**: Mandatory

**Description**: This field describes the type of authentication flow, such as a regular login or a multi-factor authentication (MFA) event. It helps standardize different event types from various sources into two clear categories - making detection logic easier to build, understand, and reuse across systems.

**Supported values**:

* `XDM_CONST.OPERATION_TYPE_AUTH_LOGIN`: Login using only a password
* `XDM_CONST.OPERATION_TYPE_AUTH_MFA`: Login that involves multi-factor authentication

**Data Model Rule example**: The following pseudocode is an example only, which must be modified to implement the logic in the correct syntax by the mapped data source to different event types.

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
xdm.event.operation =
   if eventType IN ("authentication", "oauth2", "mfa", "mfa_challenge", "mfa_verify")
 then XDM_CONST.OPERATION_TYPE_AUTH_MFA
  else if eventType IN ("session", "access_request", "iwa", "ldap")
 then XDM_CONST.OPERATION_TYPE_AUTH_LOGIN
  else if is_null(eventType)
 then null  else to_string(eventType)
```
{% endcode %}

### 9. xdm.event.original\_event\_type\*

**Authentication Story Field**: `sso_event_type`

**Type**: string

**Requirement**: Mandatory

**Description**: This field captures the original name or label of the event as it appears in the raw log source. It serves as a direct reflection of the source-specific event type and is essential for maintaining source context.

**Example values**:

* `user.authentication.sso`_(Okta – SSO authentication event)_
* `user.mfa.okta_verify.push.deny`_(Okta – MFA denied)_
* `user.session.start`_(Okta – Session initiated)_
* `microsoft.login.success`_(Azure AD – Successful login)_
* `microsoft.mfa.challenge.fail`_(Azure AD – MFA failure)_
* `google.sign_in.challenge`_(Google Workspace – Sign-in challenged)_
* `user.lockout`_(Generic – Account locked due to failed attempts)_

### 10. xdm.auth.service\*

**Authentication Story Field**: `auth_service`

**Type**: string

**Requirement**: Mandatory

**Description**: This field defines the **role** the system played in the authentication flow for this specific record.

**Supported values**:

* **IDP**: Use when the system validates the credential (such as Okta, Entra ID, Domain Controller).
* **SP**: Use when the system initiates the request and relies on another to validate (such as a relying-party app consuming SSO).
* **Universal**: Use when the source is NOT a known IdP provider (such as local accounts, TACACS+, RADIUS, device SSH).

**Data Model Rule example for Okta**:

```programlisting
if(eventType = "user.authentication.auth_via_AD_agent", "IDP",
 eventType = "user.authentication.auth_via_radius", "IDP", ..., eventType = "user.authentication.sso", "SP", null)
```

{% hint style="info" %}
### Note

Mapping should be done per event type. The same system could be an IDP in one event and an SP in another. NEVER use a service or protocol name like "Kerberos", "SSH", or "Login" in this field. Mapping should be done per event type. The same system could be an IDP in one event and an SP in another.
{% endhint %}

### 11. xdm.event.outcome\*

**Authentication Story Field**: `auth_outcome`

**Type**: string (ENUM)

**Requirement**: Mandatory

**Description**: Specifies the final result of the authentication attempt. Use values such as `OUTCOME_SUCCESS` or `OUTCOME_FAILURE` only for events that definitively represent the conclusion of the authentication process, such as when access is explicitly granted or denied. Avoid assigning these values to intermediate steps that don’t reflect the outcome.

**Supported values**:

* `XDM_CONST.OUTCOME_SUCCESS`
* `XDM_CONST.OUTCOME_FAILED`

{% hint style="info" %}
### Note

For more information on the event outcome constants in the Cortex Data Model, see [XDM\_CONST.OUTCOME](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/consts/outcome).
{% endhint %}

**Data Model Rule example logic**:

```programlisting
if(res ~= "[Ss]uccess" OR res = "sent",
 XDM_CONST.OUTCOME_SUCCESS, res ~= "fail",
 XDM_CONST.OUTCOME_FAILED)
```

{% hint style="info" %}
### Note

Outcome is based on a conclusive event type reflecting the true end state of the authentication `flow.Critical` for the effectiveness of detection rules. Incorrect derivation can lead to missed detections or false positives.
{% endhint %}

## Optional fields

<details>

<summary>Outcome details</summary>

#### 12. xdm.event.outcome\_reason

**Authentication Story Field**: `auth_outcome_reason_category`

**Type**: string

**Requirement**: Optional

**Description**: Specifies a standardized and descriptive reason for the outcome of an authentication or access-related event. This field offers detailed context beyond a simple success or failure result and is essential for accurate risk assessment, efficient triage, and effective incident response.

**Supported values**:

* `user_does_not_exist`
* `bad_credentials`
* `account_expired_or_disabled`
* `account_locked`
* `failed_login`
* `auth_policy_access_violation`
* `mfa_failure`
* `mfa_expired`
* `user_reject`
* `user_cancelled`
* `OTHER`
* `NOT_SPECIFIED`

**Required action**: Explicit mapping logic is required between the raw event fields that contain outcome/error messages, such as `get_reason` and `debug_data_error_code`, and this canonical field. Mapping must normalize provider-specific strings or error codes into one of the supported values.

**Data Model Rule example**: The following pseudocode is an example only, which must be modified to implement the logic in the correct syntax.

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
xdm.event.outcome_reason = if(  get_reason ~= "UNKNOWN_USER",                        "user_does_not_exist",
  get_reason ~= "Login denied. No matching user",      "user_does_not_exist",
  get_reason ~= "INVALID_CREDENTIALS",                 "bad_credentials",  debugdata_errorcode ~= "1326",                       "bad_credentials",
  get_reason ~= "account is expired",                  "account_expired_or_disabled",
  get_reason ~= "USER_ACCOUNT_EXPIRE",                 "account_expired_or_disabled",  debugdata_errorcode IN ("1331", "1793"),             "account_expired_or_disabled",
  get_reason ~= "account is locked",                   "account_locked",
  get_reason ~= "LOCKED_OUT",                          "account_locked",
  get_reason ~= "Login failed",                        "failed_login",
  get_reason ~= "PASSWORD_BASED_LOGIN_DISALLOWED",     "auth_policy_access_violation",
  get_reason ~= "login denied",                        "auth_policy_access_violation",
  get_reason ~= "VERIFICATION_ERROR",                  "mfa_failure",
  get_reason ~= "DEL_AUTH_TIMEOUT",                    "mfa_expired",
  get_reason ~= "User rejected Okta push verify",      "user_reject",
  get_reason ~= "Login aborted",                       "user_cancelled",
  get_reason ~= "NOT_SPECIFIED",                       "OTHER")
```
{% endcode %}

</details>

<details>

<summary>Authentication identity and context</summary>

#### 13. xdm.source.user.upn\*

**Authentication Story Field**: `auth_identity`

**Type**: string

**Requirement**: Mandatory

**Description**: Represents the user identity associated with the authentication or access event. This field must be populated using the User Principal Name (UPN) format. It cannot be left empty.

Using UPN as a normalized identity format ensures consistency across diverse identity providers, such as Azure AD, Okta, and on-prem AD, and authentication flows. It plays a central role in correlating activity across logs, enriching detections, and building an accurate authentication story across systems.

**Example values**: `jane.doe@company.com`

#### 14. xdm.event.description

**Authentication Story Field**: `sso_display_message`

**Type**: string

**Requirement**: Optional

**Description**: Provides a human-readable summary describing the nature of the authentication event. This value is typically derived from the source system's descriptive message and is intended to offer clear context for analysts during monitoring and investigations.

**Example values**:

* `“A push was sent to a user for verification”`
* `"User single sign on to app”`
* `“Authentication of user via MFA”`

</details>

<details>

<summary>Device and authentication method</summary>

#### 15. xdm.source.host.device.id

**Authentication Story Field**: `agent_id`

**Type**: string

**Requirement**: Optional

**Description**: This field represents the unique identifier of the device that initiated or is associated with the current authentication event.

The value should remain consistent per device over time and be mapped from the most reliable source-specific field, such as device ID, machine ID, or equivalent. If there isn't a sufficient device ID field, the alternative will be to map the IP address that initiated the authentication (same as `xdm.source.ipv4`).

#### 16. xdm.source.host.hostname

**Authentication Story Field**: `auth_device_name`

**Type**: string

**Requirement**: Optional

**Description**: Represents the host/device name associated with the authentication event that initiated or is responsible for authentication events.

#### 17. xdm.logon.type

**Authentication Story Field**: `auth_is_interactive`

**Type**: string

**Requirement**: Optional

**Description**: Represents the type of logon associated with the authentication event, with a focus on distinguishing between interactive (user-driven) and non-interactive (system or service-based) activity. This distinction is important for behavioral analysis, risk scoring, and threat detection.

**Common values**:

* `XDM_CONST.LOGON_TYPE_INTERACTIVE`: Indicates a user is interactively using the machine, such as logging in through a terminal session, remote shell, or console.
* `XDM_CONST.LOGON_TYPE_SERVICE`: Indicates a service-type logon, such as Windows service, automations, and application tokens, where the account must have the service logon privilege.

{% hint style="info" %}
### Note

These are the most common values, but other logon types also exist. For a complete list, see [XDM\_CONST.LOGON\_TYPE](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/consts/logon-type).
{% endhint %}

#### 18. xdm.event.operation.sub\_type

**Authentication Story Field**: `auth_method`

**Type**: string

**Requirement**: Optional

**Description**: Specifies a standardized and descriptive reason for the outcome of an authentication or access-related event. This field offers detailed context beyond a simple success or failure result and is essential for accurate risk assessment, efficient triage, and effective incident response.

**Required action**: You must define explicit mapping logic between the raw field in the source log that contains the authentication method information, such as `authMethod`, `authenticationFlow.type`, and `factorUsed`, and this XDM field.

This mapping should translate raw values into one of the allowed sub-category listed below.

**Data Model Rule example**: The following pseudocode is an example only, which must be modified to implement the logic in the correct syntax.

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
if(lowercase_auth_method = "password",       "password",
   lowercase_auth_method = "otp_sms",        "sms",
   lowercase_auth_method = "push",           "application",
   lowercase_auth_method = "yubikey",        "hardware_token",
   lowercase_auth_method = "trusted_device", "trusted_login",
   lowercase_auth_method = "sso",            "Generic SSO",
   lowercase_auth_method = "email",          "email",
   lowercase_auth_method = "voice",          "voice",
   lowercase_auth_method = null,             null,   to_string(lowercase_auth_method))
```
{% endcode %}

**Supported values (per applicable event type)**:

* `hardware_token`: Physical device-based authentication, such as RSA token or YubiKey.
* `password` : Standard password-based login.
* `application`: Action approved via an authenticator app, such as push notification.
* `email`: Verification through email link or one-time code.
* `sms`: SMS-based one-time password (OTP) or verification.
* `voice`: Verification via voice call.
* `trusted_login`: Login from a known or previously trusted device.
* `Generic SSO`: Federated authentication using a standard single sign-on provider.
* `null`: No sub-type specified or not applicable.

</details>

<details>

<summary>User identity attributes</summary>

#### 19. xdm.source.user.identifier

**Authentication Story Field**: `auth_identity_id`

**Type**: string

**Requirement**: Optional

**Description**: This field should contain a unique and consistent identifier for the user associated with the event.

**Example values**:

* `a1b2c3d4-e5f6-7890-ab12-3456789cdef0`: Directory object GUID, such as Azure AD object ID.
* `S-1-5-21-3623811015-3361044348-30300820-1013`: Windows Security Identifier (SID).

**Best Practice**: Populate with the most persistent and canonical user identifier available from the identity source.

#### 20. xdm.source.user.username

**Authentication Story Field**: `auth_identity_display_name`

**Type**: string

**Requirement**: Optional

**Description**: User Display Name Field. This field should contain the user's name in a human-readable format, typically including the first and last name, such as John Smith.

#### 21. xdm.source.user.user.type

**Authentication Story Field**: `auth_normalized_user.identity_type`

**Type**: string

**Requirement**: Optional

**Description**: Indicates the type of identity associated with the authentication event.

**Supported values (Constants)**:

* `XDM_CONST.USER_TYPE_REGULAR ("USER")`
* `XDM_CONST.USER_TYPE_SERVICE_ACCOUNT ("SERVICE ACCOUNT")`
* XDM\_CONST.USER\_TYPE\_MACHINE\_ACCOUNT ("MACHINE ACCOUNT")

**Example mapping logic**: The following pseudocode is an example only, which must be modified to implement the logic in the correct syntax.

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
if(actor_type in("User"), XDM_CONST.USER_TYPE_REGULAR, actor_type
 in("SystemPrincipal"),
 XDM_CONST.USER_TYPE_SERVICE_ACCOUNT,actor_type in("IP address"),
 XDM_CONST.USER_TYPE_MACHINE_ACCOUNT, to_string(actor_type))
```
{% endcode %}

{% hint style="info" %}
### Note

For more information, see [XDM\_CONST.USER\_TYPE](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/consts/user-type).
{% endhint %}

#### 22. xdm.auth.privilege.level

**Authentication Story Field**: `auth_normalized_user.privilege_level`

**Type**: string

**Requirement**: Optional

**Description**: Represents the privilege level or role of the user during the authentication event, such as admin, user, or guest. Used to assess risk and impact. Should reflect a canonical privilege level.

**Supported values (Constants)**:

* `XDM_CONST.PRIVILEGE_LEVEL_GUEST`
* `XDM_CONST.PRIVILEGE_LEVEL_USER`
* `XDM_CONST.PRIVILEGE_LEVEL_ADMIN`
* `XDM_CONST.PRIVILEGE_LEVEL_SYSTEM`

**Example mapping logic**: The following pseudocode is an example only, which must be modified to implement the logic in the correct syntax.

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
if(lowercase_user_type = "user", XDM_CONST.PRIVILEGE_LEVEL_USER,
 lowercase_user_type = "guest", XDM_CONST.PRIVILEGE_LEVEL_GUEST,
 lowercase_user_type = "admin", XDM_CONST.PRIVILEGE_LEVEL_ADMIN,
 lowercase_user_type = "system", XDM_CONST.PRIVILEGE_LEVEL_SYSTEM,
 lowercase_user_type = null, null, to_string(lowercase_user_type))
```
{% endcode %}

{% hint style="info" %}
### Note

For more information, see [XDM\_CONST.PRIVILEGE\_LEVEL](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/consts/privilege-level).
{% endhint %}

</details>

<details>

<summary>Target and session context</summary>

#### 23. xdm.target.resource.id

**Authentication Story Field**: `auth_target_id`

**Type**: string

**Requirement**: Optional

**Description**: Represents the unique identifier of the accessed resource or application during the authentication event, such as application ID or internal resource ID.

#### 24. xdm.target.resource.name

**Authentication Story Field**: `auth_target`

**Type**: string

**Requirement**: Optional

**Description**: Provides the readable name of the resource or application accessed during the event. This should reflect the logical service or platform the user interacted with.

**Example values**: `״Exchange", ״SharePoint״, ״ServiceNow״, ״HR Portal״, ״Okta Admin Portal״`

#### 25. xdm.source.user.agent

**Authentication Story Field**: `action_user_agent`

**Type**: string

**Requirement**: Optional

**Description**: Captures the full user-agent string from the client initiating the authentication request. Typically includes information about the browser, operating system, device type, and version details.

**Example values**: `“Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.6312.86 Safari/537.36”`

#### 26. xdm.network.session\_id

**Authentication Story Field**: `sso_debug_data.session_id`

**Type**: string

**Requirement**: Optional

**Description**: Represents the session identifier associated with the user interaction. This value is typically issued by the application or identity platform and is used to group multiple related actions or requests made by the same user or device within a defined time window, commonly referred to as a session.

These can include login, token refresh, or other events that occur as part of a continuous authenticated interaction.

**Example use cases**:

* Tracking session duration
* Linking session start and end events
* Grouping multiple MFA prompts within a single login session

</details>

<details>

<summary>Source location</summary>

#### 27. xdm.source.location.city

**Authentication Story Field**: `action_location.city`

**Type**: string

**Requirement**: Optional

**Description**: Represents the city associated with the source IP address.

#### 28. xdm.source.location.country

**Authentication Story Field**: `action_location.country`

**Type**: string

**Requirement**: Optional

**Description**: Identifies the country where the authentication request originated, based on the source IP address.

**Example values**: `“US,“ “IL“, “DE“, “FRANCE”`

#### 29. xdm.source.location.region

**Authentication Story Field**: `action_location.region`

**Type**: string

**Requirement**: Optional

**Description**: Captures the region, province, or state associated with the source IP address.

**Example values**: `“California“, “Bavaria“, “Tel Aviv“`

#### 30. xdm.source.location.latitude

**Authentication Story Field**: `action_location.latitude`

**Type**: float

**Requirement**: Optional

**Description**: Represents the latitude coordinate of the source IP address's estimated physical location.

**Example values**: `“40.7128”, “48.8566”`

#### 31. xdm.source.location.longitude

**Authentication Story Field**: `action_location.longitude`

**Type**: float

**Requirement**: Optional

**Description**: Represents the longitude coordinate of the source IP address's estimated physical location.

#### 32. xdm.source.location.continent

**Authentication Story Field**: `action_location.continent`

**Type**: string

**Requirement**: Optional

**Description**: Indicates the continent associated with the source IP's location, such as Europe, Asia, or North America.

#### 33. xdm.source.location.timezone

**Authentication Story Field**: `action_location.timezone`

**Type**: string

**Requirement**: Optional

**Description**: This enables time-based correlation between user activity and local context.

**Example values**: `"Asia/Jerusalem", "America/New_York", "UTC"`

</details>

<details>

<summary>Client device and operating system</summary>

#### 34. xdm.source.host.device.category

**Authentication Story Field**: `auth_client_type`

**Type**: string

**Requirement**: Optional

**Description**: Represents the operating system family of the device or client that initiated the event.

**Supported values**:

* `“Computer”`: A desktop or laptop device.
* `“Mobile”`: A mobile phone or smartphone.
* `“IOT”`: An Internet of Things device, such as smart TV or smart speaker.
* `“Tablet”`: A tablet computing device.

#### 35. xdm.source.application.name

**Authentication Story Field**: `agent_extra_data.browser`

**Type**: string

**Requirement**: Optional

**Description**: Represents browser vendor used during the authentication event.

**Example values**: `“Chrome“, “Firefox“, “Safari“, “Edge“`

#### 36. xdm.source.application.version

**Authentication Story Field**: `agent_extra_data.browser_version`

**Type**: string

**Requirement**: Optional

**Description**: Represents the version of the browser used during the authentication event.

**Example values**: `“Chrome 113“, “Firefox 102“, “Safari 16.3“`

#### 37. xdm.source.host.os.family

**Authentication Story Field**: `agent_os_type`

**Type**: string

**Requirement**: Optional

**Description**: Provides a normalized, high-level abstraction of the operating system associated with the source host. This field enables consistent behavior across different data sources.

**Required action**: You must explicitly define a mapping logic between the raw field in the original data source that contains the OS information, such as `device.os_name`, and normalize into the XDM field.

**Common values (Constants)**:

* `XDM_CONST.OS_FAMILY_WINDOWS`
* `XDM_CONST.OS_FAMILY_MACOS`
* `XDM_CONST.OS_FAMILY_LINUX`
* `XDM_CONST.OS_FAMILY_ANDROID`
* `XDM_CONST.OS_FAMILY_IOS`

{% hint style="info" %}
### Note

For more information, see [XDM\_CONST.OS\_FAMILY](https://app.gitbook.com/s/HVBaxKOW1b6qcIQ6iMBh/consts/os-family).
{% endhint %}

**Example mapping logic**: The following pseudocode is an example only, which must be modified to implement the logic in the correct syntax.

{% code expandable="true" collapsedlinecount="3" %}
```programlisting
if raw_event.host_os contains "windows"      → XDM_CONST.OS_FAMILY_WINDOWS  
if raw_event.host_os contains "mac"          → XDM_CONST.OS_FAMILY_MACOS  
if raw_event.host_os contains "linux"        → XDM_CONST.OS_FAMILY_LINUX  
if raw_event.host_os contains "android"      → XDM_CONST.OS_FAMILY_ANDROID  
if raw_event.host_os contains "ios"          → XDM_CONST.OS_FAMILY_IOS  
```
{% endcode %}

**Data Model Rule example logic**:

```programlisting
 if(os contains "windows", XDM_CONST.OS_FAMILY_WINDOWS, os contains "mac", XDM_CONST.OS_FAMILY_MACOS, ...)
```

#### 38. xdm.source.host.os

**Authentication Story Field**: `agent_os_sub_type`

**Type**: string

**Requirement**: Optional

**Description**: This field captures the raw operating system information reported by the source host's telemetry.

**Example values**: `“Microsoft Windows NT 10.0“, “Microsoft Windows NT 6.1 (Windows 7“), “Darwin Kernel Version 20.6.0“`

</details>

<details>

<summary>Time and request correlation</summary>

#### 39. xdm.session.context.id

**Authentication Story Field**: `auth_correlation_id`

**Type**: string

**Requirement**: Optional

**Description**: Represents a correlation ID tied to a single authentication or access-related request. This ID is generated by the identity provider, such as Azure AD or Okta, and used to link events belonging to a single logical transaction, such as an SSO login flow or token issuance.

**Example values**: `”25423545-6364-5423-3232-42343760”`

{% hint style="info" %}
### Note

While `xdm.network.session_id` aggregates multiple user actions within a broader session window. `xdm.session.context.id` is used to correlate events that belong to a single authentication request or transaction.
{% endhint %}

#### 40. xdm.time

**Authentication Story Field**: `generatedTime`

**Type**: timestamp

**Description**: Represents the timestamp of when the event occurred. This field is essential for event sequencing and correlation. This field is automatically mapped.

**Example values**:

```programlisting
- ”2025-05-26T14:45:32Z” (UTC format ISO 8601)
- “2025-05-26T14:45:32.123Z “ (UTC with millisecond precision),
-“2025-05-26 14:45:32” (Standard datetime format non-ISO)
```

</details>
