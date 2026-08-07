---
description: Learn more about Cortex XSIAM Parsing Rules.
---

# Parsing Rules

**What are Parsing Rules?**

{% hint style="warning" %}
### Prerequisite

Parsing Rules requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Dataset Management, Data Model Rules, and Event Forwarding.
{% endhint %}

Cortex XSIAM includes an editor for creating 3rd party Parsing Rules, which enables you to:

* Remove unused data that is not required for analytics, hunting, or regulation.
* Reduce your data storage costs.
* Pre-process all incoming data for complex rule performance.
* Add tags to the ingested data as part of the ingestion flow.
* Easily identify and resolve Parsing Rules errors so you can troubleshoot them quickly.
* Test your Parsing Rules on actual logs and validate their outputs before implementation.

Parsing Rules contain the following built-in characteristics:

* Parsing Rules are bound to a specific vendor and product.
* Parsing Rules take raw log input, perform an arbitrary number of transitions and modifications to the data using Cortex Query Language (XQL), and return zero, one, or more rows that are eventually inserted into the Cortex XSIAM tenant.
* Parsing Rules can be grouped together by a no-match policy. If all the rules of a group did not produce an output for a specific log record, a no-match policy defines what to do, such as drop the log or keep the log in some default format.
* Upon ingestion, all fields are retained even fields with a null value. You can also use XQL to query parsing rules for null values.
