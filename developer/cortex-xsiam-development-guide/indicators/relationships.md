---
description: Cortex XSIAM guidance for creating indicator relationships during enrichment.
---

# Relationships

The `create_relationships` parameter in integrations creates relationships between indicators.

```programlisting
- defaultvalue: 'true'
  additionalinfo: Create relationships between indicators as part of enrichment.
  display: Create relationships
  name: create_relationships
  required: false
  type: 8
```

#### To create a relationship:

1.  Create an `EntityRelationship` object with the relationship's data. If more than one relationship exists, create a list and append all of the `EntityRelationship` objects to it.

    ```programlisting
    EntityRelationship(
       name='contains',
       entity_a='1.1.1.1',
       entity_a_type='IP',
       entity_b='2.2.2.2',
       entity_b_type='IP',
       source_reliability='B - Usually reliable',
       brand='My Integration ID')
    ```
2. When setting the name of the relationship, choose a value that appears in the the predefined list of [relationships](https://xsoar.pan.dev/docs/reference/api/common-server-python#relationships.).
3. Use the `Common` object when creating the indicator and in the relationships key set the list of `EntityRelationship` objects.
4. Use `CommandResults` to set the relationships key to the list of `EntityRelationship` objects.

For more information about creating a relationship entity, see [EntityRelationship](https://xsoar.pan.dev/docs/reference/api/common-server-python#entityrelationship).

#### Example integrations

* [AlienVault OTX](https://github.com/demisto/content/tree/master/Packs/AlienVault_OTX)
* [MISP](https://github.com/demisto/content/tree/master/Packs/MISP/Integrations/MISP_V2)
* [DeHashed](https://github.com/demisto/content/tree/master/Packs/DeHashed/Integrations/DeHashed)
