# Expected results when querying fields

The following are returned when querying fields:

* If specific fields are stated in the [fields](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/fields) stage, those exact fields will be returned.
* If no fields are stated in the query, the `xdm_core` fieldset will be returned.
* Unmapped fields are treated as NULL. An unmapped field is a `xdm` field that hasn't been mapped from the relevant datasets using a Data Model Rule.
* By default, the `_time` system field will be added to all data model queries. Yet, the `_time` system field will not be added to queries that contain the `comp` stage.
* For dataset queries, all current system fields will be returned, even if they are not stated in the query.
* For UNION between XDM and dataset, each part of the UNION will return its own fields.
* Each new column in the result set created by the [alter](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/alter) stage will be added as the last column. You can specify a different column order by modifying the field order in the [fields](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/fields) stage of the query.
* Each new column in the result set created by the [comp](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/comp) stage will be added as the last column. Other fields that are not in the `group by / calculated` column will be removed from the result set, including the core fields and `_time` system field.
* When no limit is explicitly stated in a `datamodel` query, a maximum of 1000 results are returned (default). When this limit is applied to results using the [limit](https://app.gitbook.com/s/fUtoMSNyY2P8jbK3cQsM/readme/stages/limit) stage, it will be indicated in the user interface.
