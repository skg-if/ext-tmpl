---
title: New entity
parent: Extended interoperability framework
layout: default
nav_order: 3
---

# New entity

Describe here the properties and relations of [New entity] introduced by this extension.
Like any other entity in the SKG-IF, [New entity] has to have some basic mandatory fields for identification and for its type.


## Properties

### `local_identifier`
*String* (mandatory): Unique code identifying the [New entity] in the SKG (if any, otherwise "stateless identifier").

**Suggestion:** Use a URL as a string to make this entity dereferenceable on the Web. For additional information, see the [section 'Local identifiers of entities' of the Interoperability Framework](/interoperability-framework/#local-identifiers-of-entities).

```json
    "local_identifier": "https://w3id.org/oc/meta/ra/0614010840729"
```

### `identifiers`

*List* (recommended): A list of objects representing external identifiers for the entity. 
Each object is structured as follows:
- `scheme` *String* (mandatory): The scheme for the external identifier (e.g., orcid, viaf, etc.).
- `value` *String* (mandatory): The external identifier.

{: .important }
The current version of SKG-IF includes the following types of identifiers (to be specified as strings in the field “scheme”): `orcid`, `viaf`, ...

```json
    "identifiers": [
        {
            "scheme": "orcid",
            "value": "0000-0002-5193-7851"
        }           
    ]
```

### `entity_type`
*String* (mandatory): Field stating what kind of entity is being serialised. Needed for parsing purposes; fixed to `ext:my_entity`. Please notice that you need to prepend the assigned `ext_` prefix to your type in order to prevent possible clashes with other extensions.

```json
    "entity_type": "ext_new_entity"
```

### `ext_attribute`
*Type* (optional|recommended|mandatory): attribute description.

```json
    "ext_attribute": "value"
```

----
[New entity]: {% link extension-template/extended-interoperability-framework/extension-entities/ext-new-entity.md %}