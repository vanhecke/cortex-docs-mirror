# Lookup datasets

{% hint style="warning" %}
### Prerequisite

Dataset Management requires **View/Edit** RBAC permissions for **Data Management** (under **Configurations** → **Data Management**), which are the same permissions required for Parsing Rules, Data Model Rules, and Event Forwarding.
{% endhint %}

Lookup datasets enable you to correlate data from a data source you provide with the events in your environment. For example, you can create a lookup with a list of high-value assets, terminated employees, or service accounts in your environment. Use lookups in your search, detection rules, threat hunting, and response playbooks. Lookups are stored as name-value pairs and are cached for optimal query performance and low latency.

Lookup tables support low-frequency changes of up to 1200 modifications per day. Changes are implemented whenever a lookup dataset is edited, where only one person or user can edit the file at a given time. Concurrent users editing the file are not supported.

<details>

<summary>Use case scenarios</summary>

* Investigate threats and respond to cases quickly with the rapid import of IP addresses, file hashes, and other data from CSV files. After you import the data, use lookup name-value pairs for joins and filters in threat hunting and general queries.
* Import business data as a lookup. For example, import user lists with privileged system access, or terminated employees. Then, use the lookup to create allow lists and blocklists to detect or prevent those users from logging in to the network.
* Create allow lists to suppress issues from a group of users, such as users from authorized IP addresses that perform tasks that would normally trigger the issue. Prevent benign events from becoming issues.
* Enrich event data. Use lookups to enrich your event data with name-value combinations derived from external data sources.

</details>

<details>

<summary>How are lookup datasets created?</summary>

You can import or create a lookup dataset, and then reference the values for a certain key, run queries, and take action. Lookup datasets are created by any of the following methods:

* Manual upload from a CSV, TSV, or JSON file to Cortex XSIAM from the **Dataset Management** page. For more information, see [Import a lookup dataset](import-a-lookup-dataset).
* Automatic upload by the Files and Folders Collector.
*   Query results are saved to a lookup dataset. If saved using the **`target`** stage, the **Type** can be either **User** or **Lookup**. For more information, see the `target` stage.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Important</h3><p>When you create or add data to a lookup dataset using the <code>target</code> stage, the <code>_time</code> field won't be included by default unless you explicitly add it with the <code>fields</code> stage.</p></div>

After a lookup, a dataset is imported, you can always edit the dataset to update the data manually by right-clicking the dataset and selecting **Edit**.

{% hint style="info" %}
### Note

A lookup dataset can only be deleted if there are no other dependencies. For example, if a Correlation Rule is based on a lookup dataset, you wouldn't be able to delete the lookup dataset until you removed the dataset from the XQL query of the Correlation Rule.
{% endhint %}

</details>
