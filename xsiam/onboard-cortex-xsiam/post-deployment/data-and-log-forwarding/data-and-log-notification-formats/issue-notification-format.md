# Issue notification format

Issues can be forwarded to the following:

* Email distribution list
* Syslog server
* Slack
* Splunk, Amazon SQS, Amazon S3, or Webhook

{% hint style="info" %}
For issues with relevant assets, issue notifications sent to Amazon S3, Amazon SQS, Webhook, Splunk, and email provide asset and remediation information including the asset name, cloud resource name, asset tags, account name, region, and evidence.
{% endhint %}

**Email account**

Cortex XSIAM sends issues to email accounts based on the settings you configure. Email messages also include an issue code snippet of the fields according to the columns in the Issue table.

The notification format is as follows:

* If only one issue exists in the queue, a single-issue email format is sent.
* If more than one issue was grouped in the time frame, all the issues in the queue are forwarded together in a grouped email format.

**Example**

Single-issue email message

```
Email Subject: Issue: <issue_name>
	Email Body:
	    Issue Name: Suspicious Process Creation
	    Severity: High
	    Source: Correlation
	    Category: Malware 
	    Action: Detected
	    Host: <host name>
	    Username:<user name>
	    Excluded: No
	    Starred: Yes 
	    Issue: <link to the tenant issue view>
	    Case: <link to the tenant case view>
```

\
**Example**

Single-issue email message with asset

```
Email Subject: Issue: <issue_name>
	Email Body:
	    Issue Name: Suspicious Process Creation
	    Severity: High
        Remediation: N/A
       Initial Evidence: N/A
        Asset 1:
           Asset ID: e2c48011383e2d606d66e564d7ca523e638422f90c1dc09ae33af9015d8afd17
           Asset Name: holodeck_agent-d40088a128624a
           Asset Account: Other
           Asset External Provider ID: N/A
           Asset Tags: N/A
        Source: Correlation
	    Category: Malware 
	    Action: Detected
	    Host: <host name>
	    Username:<user name>
	    Excluded: No
	    Starred: Yes 
	    Issue: <link to the tenant issue view>
	    Case: <link to the tenant case view>
```

\
**Example**

Grouped issue email message

```
Email Subject: Issues: <first_highest_severity_issue> + x others
	Email Body:
	   Issue Name: Suspicious Process Creation
	   Severity: High
	   Source: Correlation
	   Category: MalwareAction: Detected
	   Host: <host name>
	   Username:<user name>
	   Excluded:No
	   Starred: Yes
	   Issue: <link to the tenant issue view>
           Case: <link to the tenant case view>
	   Issue Name: Behavioral Threat Protection
	   Issue ID: 2412
	   Description: A really cool detection
	   Severity: Medium
	   Source: Correlation
	   Category: Exploit
	   Action: Prevented
	   Host: <host name>
	   Starred: Yes
	   Case: <link to the tenant issue view>
	   Issue: <link to the tenant case view>
	   Notification Name: “My notification policy 2 ”
	   Notification Description: “Starred issues with medium severity”
```

\
**Example**

Email attachment

```
{
    "original_issue_json":{
        "uuid":"<UUID Value>",
        "recordType":"threat",
        "customerId":"<Customer ID>",
        "severity":4,
        "...",
        
    "is_pcap":null,
    "contains_featured_host":[
        "NO"
    ],
    "contains_featured_user":[
        "YES"
    ],
    "contains_featured_ip":[
        "YES"
    ],
    "events_length":1,
    "is_excluded":false
    
}
```

\
**Example**

Email attachment with asset

```
{
  "agent_id": null,
  "category": "POSTURE",
  "observation_time": 1776826363623,
  "is_excluded": false,
  "mitre_tactics": null,
  "mitre_techniques": null,
  "owner": "AISPM",
  "detection.rule_id": "90bed230-210a-42ec-880a-86edb934ec0f",
  "detection.method": "AISPM_RULE_ENGINE",
  "is_starred": false,
  "original_issue_json": {
    "xdm.issue.detection.method": "AISPM_RULE_ENGINE",
    "issues": [
      {
        "xdm.issue.detection.rule_id": "90bed230-210a-42ec-880a-86edb934ec0f",
        "xdm.issue.detection.method": "AISPM_RULE_ENGINE",
        "xdm.issue.platform_status.progress": "NEW",
        "xdm.issue.external_id": "90bed230-210a-42ec-880a-86edb934ec0f:342799b2aaf50ae1e3efb9beb5efc12f22ea197817a2a4e586402d79ef7f2e23",
        "xdm.issue.name": "DP - custom AI 04/21",
        "xdm.issue.description": "DP - custom AI 04/21",
        "xdm.issue.platform_severity": "CRITICAL",
        "xdm.issue.asset_ids": [
          "342799b2aaf50ae1e3efb9beb5efc12f22ea197817a2a4e586402d79ef7f2e23"
        ],
        "xdm.issue.auto_resolve_findings": false,
        "xdm.issue.auto_resolve_assets": false,
        "xdm.issue.extended_fields": {}
      },
      {
        "xdm.issue.detection.rule_id": "90bed230-210a-42ec-880a-86edb934ec0f",
        "xdm.issue.detection.method": "AISPM_RULE_ENGINE",
        "xdm.issue.platform_status.progress": "NEW",
        "xdm.issue.external_id": "90bed230-210a-42ec-880a-86edb934ec0f:4f4e4635688677ac8d03457f2e310d77e67510fc52d797f963d69c21a5055e86",
        "xdm.issue.name": "DP - custom AI 04/21",
        "xdm.issue.description": "DP - custom AI 04/21",
        "xdm.issue.platform_severity": "CRITICAL",
        "xdm.issue.asset_ids": [
          "4f4e4635688677ac8d03457f2e310d77e67510fc52d797f963d69c21a5055e86"
        ],
        "xdm.issue.auto_resolve_findings": false,
        "xdm.issue.auto_resolve_assets": false,
        "xdm.issue.extended_fields": {}
      }
      /* ... 18 additional issue objects omitted for brevity ... */
    ],
    "__group_during_create": false,
    "__action": "upsert",
    "xdm.issue.observation_time": 1776826363623,
    "xdm.issue.category": "POSTURE",
    "xdm.issue.domain": "POSTURE"
  },
  "id": 17276,
  "issue_domain": "DOMAIN_POSTURE",
  "external_id": "90bed230-210a-42ec-880a-86edb934ec0f:34afc3ebd42363afbbb0269642f909696fda8658f21465f9002c7130dd62154b",
  "severity": "SEV_050_CRITICAL",
  "platform_severity": "SEV_050_CRITICAL",
  "matching_status": "UNMATCHABLE",
  "_insert_time": 1776828440454,
  "name": "DP - custom AI 04/21",
  "description": "DP - custom AI 04/21",
  "dispatch_state": "DISPATCHABLE",
  "issue_type": "Unclassified",
  "resolution_status": "STATUS_010_NEW",
  "tags": [
    {
      "tag_id": "DOM:5",
      "tag_name": "DOM:Posture"
    },
    {
      "tag_id": "DS:PANW/AI Security Posture",
      "tag_name": "DS:PANW/AI Security Posture"
    }
  ],
  "platform_status.progress": "STATUS_010_NEW",
  "status.progress": "STATUS_010_NEW",
  "legacy_fields": {
    "alert_action_status": "SCANNED",
    "contains_featured_host": [
      "NO"
    ],
    "contains_featured_ip": [
      "NO"
    ],
    "contains_featured_user": [
      "NO"
    ],
    "emailsentsuccessfully": false,
    "exported": false,
    "feedBased": false,
    "hasRole": false,
    "passwordresetsuccessfully": false,
    "retained": false,
    "is_xsoar_alert": false,
    "is_pcap": false,
    "is_rule_triggering": false
  },
  "assets": [
    {
      "asset_name": "Nova 2 Lite",
      "asset_region": "us-east-2",
      "asset_account": "850876390271",
      "asset_id": "34afc3ebd42363afbbb0269642f909696fda8658f21465f9002c7130dd62154b",
      "asset_external_provider_id": "arn:aws:bedrock:us-east-2::foundation-model/amazon.nova-2-lite-v1:0"
    }
  ]
}
```

<br>

**Slack channel, Splunk, Amazon S3, Amazon SQS, Webhook**

You can send issue notifications to a single Slack contact or a Slack channel, or to Splunk, Amazon S3, Amazon SQS, or Webhook. Notifications are similar to the email format.

**Syslog receiver**

Issue notifications forwarded to a syslog receiver are sent in a CEF format RF 5425.

| Section       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Syslog header | `<9>: PRI (considered a priority field)1: version number2020-03-22T07:55:07.964311Z: timestamp of when alert/log was sentcortexxdr: host name`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| CEF header    | `HEADER/Vendor="Palo Alto Networks" (as a constant string)HEADER/Device Product="Cortex XDR" (as a constant string)HEADER/Product Version= Cortex XDR version (2.0/2.1....)HEADER/Severity=(integer/0 - Unknown, 6 - Low, 8 - Medium, 9 - High)HEADER/Device Event Class ID=alert sourceHEADER/name =alert name`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| CEF body      | `end=timestamp shost=endpoint_name deviceFacility=facility cat=category externalId=external_id request=request cs1=initiated_by_process cs1Label=Initiated by (constant string) cs2=initiator_commande cs2Label=Initiator CMD (constant string) cs3=signature cs3Label=Signature (constant string) cs4=cgo_name cs4Label=CGO name (constant string) cs5=cgo_command cs5Label=CGO CMD (constant string) cs6=cgo_signature cs6Label=CGO Signature (constant string) dst=destination_ip dpt=destination_port src=source_ip spt=source_port fileHash=file_hash filePath=file_path targetprocesssignature=target_process_signature tenantname=tenant_name tenantCDLid=tenant_id CSPaccountname=account_name initiatorSha256=initiator_hash initiatorPath=initiator_path osParentName=parent_name osParentCmd=parent_command osParentSha256=parent_hash osParentSignature=parent_signature osParentSigner=parent_signer incident=incident_id act=action suser=actor_effective_username` |

**Example**

```
end=timestamp shost=endpoint_name deviceFacility=facility cat=category externalId=external_id request=request cs1=initiated_by_process cs1Label=Initiated by (constant string) cs2=initiator_commande cs2Label=Initiator CMD (constant string) cs3=signature cs3Label=Signature (constant string) cs4=cgo_name cs4Label=CGO name (constant string) cs5=cgo_command cs5Label=CGO CMD (constant string) cs6=cgo_signature cs6Label=CGO Signature (constant string) dst=destination_ip dpt=destination_port src=source_ip spt=source_port fileHash=file_hash filePath=file_path targetprocesssignature=target_process_signature tenantname=tenant_name tenantCDLid=tenant_id CSPaccountname=account_name initiatorSha256=initiator_hash initiatorPath=initiator_path osParentName=parent_name osParentCmd=parent_command osParentSha256=parent_hash osParentSignature=parent_signature osParentSigner=parent_signer incident=incident_id act=action suser=actor_effective_username
```

<br>
