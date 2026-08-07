---
description: Create and manage relationships between indicators to capture threat context.
---

# Manage indicator relationships

**Manage indicator relationships**

Indicator relationships are connections between different indicators. These relationships can be IP addresses related to one another, domains impersonating legitimate domains, etc. These relationships enable you to enhance investigations with information about indicators and how they might be connected to other issues or indicators. For example, if you have a phishing issue with several indicators, one of those indicators might lead to another indicator, which is a malicious threat actor. Once you know the threat actor, you can investigate to see the issues it was involved in, its known TTPs (tactics, techniques, and procedures), and other indicators that might be related to the threat actor. The initial issue which started as a phishing investigation immediately becomes a true positive and relates to a specific malicious entity.

Relationships are created from threat intel feeds and enrichment integrations that support the automatic creation of relationships, such as **AlienVault OTX v2** and **URLhaus**, by selecting **Create relationships** in the integration settings. Based on the information that exists in the integrations, the relationships are formed.

You can view indicator relationships by clicking on the indicator from an issue, and then from the **Quick View** window click the **Relationships** tab.

**Create indicator relationships**

You can also manually create and modify relationships, which is useful when a specific threat report comes out. For example, Unit 42’s SolarStorm report contains indicators and relationships that might not exist in your system, or you might not be aware of their connection.

If a relationship is no longer relevant, you can revoke it. This might be relevant, for example, if a known malicious domain is no longer associated with a specific IP address.

When you create a relationship, you can set the relationship type such as whether the indicator is related, attached, applied, etc. For example, a file is `attached-to` an email. The email `communicated-with` the file.

You can create relationships by adding them in a playbook, in the CLI using the `CreateIndicatorRelationship` command, or when investigating an indicator in the Threat Intel tab.

How to add an indicator relationship from an Indicator

1. Open an indicator and in the **RELATIONSHIPS** section add a relationship.
2.  In the **New Relationships** window, in Step 1, add a query by which to search for the relevant indicators.

    You can optionally limit the time range for the search.
3. Select the indicators you want to create a relationship to.
4.  In Step 2 set the relationship type.

    By default, the relationship is **related-to**. For example, IP address x.x.x.x is `related-to` IP address y.y.y.y.
5. Save the relationship.

{% hint style="info" %}
### Note

You can also add an indicator relationship from the Quick View when selecting an indicator from an issue.
{% endhint %}

**Investigate an indicator using indicator relationships**

In this example, you can see how to use the relationships feature to further your investigation.

1. When opening an issue, the severity is low, but the issue contains the following indicators:
   * File
   * IP
2.  When you click the file hash indicator, neither the **Info** nor **Relationships** tabs have any additional details. This seems to indicate that the file is harmless.

    ![relationships\_harmless-file.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-50b2b2a298bdc03e559d7901fb225a09101904eb%2Fa990b3835ad8057ba8e6aea029fa250a9d21dae4bb5cdf7fcbe0e689ef5e2158.png?alt=media)
3.  Click on the IP address indicator.

    Under the **Info** tab, you can see that the indicator was ingested from a threat intel feed. This already bears further investigation.

    ![relationships\_ipIndicator-info.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-15e84ae9312c55f5d6921c73eba61963ebe166ae%2F347ff4dcd25a3fab9fc411ea2a2aea23586f8dafdd64458df841ace582755454.png?alt=media)
4.  Go to the **Relationships** tab.

    You can see that this indicator is related to a campaign.

    ![relationships\_ipIndicator-relationships.png](https://2786854933-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FAEIjuYE3RXcIfmuQnBbm%2Fuploads%2Fgit-blob-e739d5cedc56ae9daa0b589fb938f41a0b0dcc64%2F0ccfc590510b056fb6719a9dcd41aaf93a052d1aaa1e6a15f992a49196fcb3f7.png?alt=media)

    What started as a low severity issue, has become a lot more threatening.
