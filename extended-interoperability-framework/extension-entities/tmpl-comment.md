---
title: Entity
parent: Interoperability framework
ancestor: Extension template
layout: default
nav_order: 3
nav_exclude: true
---

# Comment

Describe here the properties and relations of [Comment] introduced by this extension.
Like any other entity in the SKG-IF, [Comment] has to have some basic mandatory fields for identification and for its type.


## Properties

### `local_identifier`
*String* (mandatory): Unique code identifying the [Comment] in the SKG (if any, otherwise "stateless identifier").

**Suggestion:** Use a URL as a string to make this entity dereferenceable on the Web. For additional information, see the [section 'Local identifiers of entities' of the Interoperability Framework](/interoperability-framework/#local-identifiers-of-entities).

```json
    "local_identifier": "https://..."
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
            "scheme": "...",
            "value": "..."
        }           
    ]
```

### `entity_type`
*String* (mandatory): Field stating what kind of entity is being serialised. Needed for parsing purposes; fixed to `tmpl_comment`. Please notice that you need to prepend the assigned `tmpl_` prefix to your type in order to prevent possible clashes with other extensions.

```json
    "entity_type": "tmpl_comment"
```

### `tmpl_content`
*String* (mandatory): attribute description.

```json
    "tmpl_content": "In this paper, the authors contribute to the SoA with A, B, and C."
```

----
[Comment]: {% link extension-template/extended-interoperability-framework/extension-entities/tmpl-comment.md %}