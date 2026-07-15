---
title: API extensions
parent: Extension template
layout: default
nav_order: 7
# nav_exclude: true
---

# API extensions

{: .important }
To prevent possible clashes with other extensions, each extension is assigned a unique prefix (e.g., the acronym you provided upon requesting an extension) that you need to prepend when defining new properties and relations for core entities. For this extension, the acronym is `tmpl`.


## Expected output
In this page, please document how your extension affects the [(core) Open API specification](/api).

The effects on the Open API specification are expressed via an [**overlay**](https://learn.openapis.org/overlay/). An overlay consist of one or more actions to update the existing specification, e.g. adding a path, a schema or a property. The overlay for this template is [./ver/current/tmpl-overlay.yaml](./ver/current/tmpl-overlay.yaml).

An overlay can be applied to the existing Open API specification (the core one or one already extended with another extension) using a tool like [openapi](https://github.com/speakeasy-api/openapi), which can the also validate the resulting Open API specification:

```sh
openapi overlay apply --overlay tmpl-overlay.yaml --schema skg-if-openapi.yaml > out.yaml
openapi spec validate out.yaml
```

The extension can add **new entities with their own properties** and/or add **new properties to existing entities**. These two new type of additions need both one or more actions in the overlay.

### adding a new entity

If an extension adds a new entity to the model this entity needs a tag and 2 new paths in the Open API specification: 1) to retrieve an individual instance, e.g, `/comments/{short_local_identifier}` and 2) to retrieve all (filtered) instances, e.g., `/comments`. The following shows a large part of these actions for this template:

**NOTE**: when working on your own overlay check the latest version of the [(core) Open API specification](/api) esp. for the generic parts of the responses, i.e., the _context_ and the _meta_!

```yaml
actions:
  - target: $.tags
    update:
      - name: Comment
        description: comment operations (skg-if tmpl extension)
  - target: $.paths
    update:
      '/comments':
          get:
            tags:
              - Comment
            summary: Get list of Comments. 
            operationId: getComment
            description: |
                Get a list of `Comments`. See definition in SKG-IF [Extension template] (https://skg-if.github.io/ext-tmpl/extended-interoperability-framework/extension-entities/tmpl-comment.html) (entity_type: tmpl_comment ).
            parameters:
              - name: filter
                in: query
                description: |
                      Search filter. Format : Coma separated filter_name:filter_value elements ( filter_name_1:filter_value_1,filter_name_2:filter_value_2,filter_name_3:filter_value_3... ). Server side operator used is _AND_.
                schema:
                  type: string
                  pattern: '^(,?.+:.+)*$'
                examples : 
                  content_ex :
                    value: cf.search:excellent
                    summary : search comment which contains the word 'excellent' 
            responses:
              '200':
                description: Success
                content:
                  application/json:
                    schema:
                      properties:
                        "@context":
                            ...
                        meta:
                            ...
                        "@graph":
                            type: array
                            items:     
                              $ref: '#/components/schemas/Comment'
                      required: [ "@context", "meta", "@graph" ]    
 - target: $.paths
    update:
      '/comments/{short_local_identifier}':
        get:
          tags:
            - Comment
          summary: Get comment by id
          description: |
              Get a single `comment`. See definition in SKG-IF extension [Extension template](https://skg-if.github.io/ext-tmpl/extended-interoperability-framework/extension-entities/tmpl-comment.html) ( entity_type:tmpl_comment ).
          operationId: getCommentById
          parameters:
              - $ref : '#/components/parameters/shortLocalIdPathParam'
          responses:
            '200':
              description: Success
              content:
                # not 'application/json-ld' to be compatible with StopLight PRISM tool
                application/json: 
                  schema:
                    required: ["@context", "@graph"]
                    properties:
                      "@context":
                        ...
                      "@graph":
                        type: array
                        minItems: 1
                        maxItems: 1
                        items:
                          $ref: "#/components/schemas/Comment"
            '404':
              description: |
                Error if entity does not exist
```
*NOTE:* the _filter_ parameter is defined in a very generic manner. The specific filters that should/can be supported should be described in the examples.

In the _@graph_ part of the response the schema for the entity is referenced. So this schema also needs to be added:

```yaml
  - target: $.components.schemas
    update:
      Comment:
        type: object
        title: 'Comment'
        description: 'The Commment is an example extension'
        allOf:
        - $ref: "#/components/schemas/Entity"
        - type: object
          required: [
            "local_identifier","entity_type","product_type"
          ]
          properties:
            entity_type:
              default: "tmpl_comment"
              type: string
              x-faker:
                helpers.arrayElement: [["tmpl_comment"]]
            tmpl_content:
              type: string
              x-faker:
 ```
The _allOf_ part lists the schemas the new entity applies to: 1) this is always the generic `Entity` schema and 2) the object schema for the new entity. Combined these should exacly follow the narrative and examples given in the [data model](../data-model/).

### adding a new property to an existing entity

When the extension adds a new property to an existing entity (from the core model or from another extension) this can be added as follows:

```yaml
  - target: $.components.schemas.Product.allOf[1].properties
    update:
      tmpl_comments:
        description: "List of Comments"
        type: array
        items:
          type: string
          description: 'Comment identifiers'
```

So in the target of the action the entity schema is referenced, and from that schema its properties so the action will add the new property to it.

**NOTE:** if the existing entity will have new (convenience) filters using the new property these filters have to be described on the extension API page as the overlay action mechanism currently doesn't allow to append new documentation for the existing entity!

### Methodological considerations

To prevent the need to do multiple API requests to get the basic information of an entity a property can support _Lite_ structures next to using the `LocalIdentifierRef`, see for example the use of the `PersonLite` schema in the [(core) Open API specification](/api).