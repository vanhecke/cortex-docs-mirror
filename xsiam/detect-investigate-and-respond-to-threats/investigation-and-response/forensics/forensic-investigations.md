# Forensic investigations

Investigations are comprised of one or more data collections from endpoints within an environment. Grouping the collections within a single location enables you to focus on the endpoints relevant to your investigation. When searching for data, you can select two types of collections:

* **Hunt** collections enable you to search for a specific activity across a large number of hosts. A hunt collection provides more details about where something occurred. Examples of this type of collection are, finding which endpoints ran a piece of malware, which users accessed a particular file, or which endpoints were accessed by a specific user.
* **Triage** collections enable you to collect detailed information about specific activities that occurred on an endpoint. The triage functionality is configurable and supports the collection of all currently supported forensic artifacts, user-defined file paths, a full file listing for all of the connected drives, full event logs, and registry hives. The amount of data collected during a triage can be large, so triages are limited to ten or fewer endpoints per collection.
